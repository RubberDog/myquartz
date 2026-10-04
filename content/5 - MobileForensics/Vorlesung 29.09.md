### Infos zur APL

Aus e01 ein raw-image machen;\
xmount --in ewf i9300.e01 --cache /tmp/i9300.ovl --out raw /ewf

Partitionen betrachten:\
mmls i9300.E01

Loopdevice erstellen:\
losetup --partscan --find --show /ewf/i9300.dd

**Relevante Partitionen: UserData und Cache**

Verifizieren, ob es die richtige Partitionen ist:
```shell
fsstat /dev/loop0p12 | less
.
.
.
Last mounted on: /data
```

------------

Exkurs zum Kernel finden, ziehen, theoretisch wieder laden..

Partition mit Kernel finden:\
`binwalk /dev/loop0p5`\
extrahieren via `dd if=/dev/loop0p5 of=/tmp/boot.img bs=512 count=2000`\
zieht 1 MB

`file /tmp/boot.img`

--------------

Hier geht's weiter..

Ist ein Image mit .nandump benannt, ist es vermutlich ein YAFFS(2)\
Auch möglich, dass wir nur eine Partition erhalten.\

`mmls` kein Ergebnis  -> (vermutlich) kein volles image.\
`fsstat` sollte bei einer einzigen Partition ein Ergebnis liefern.

`fls` auf eine Partition sollte den Dateiinhalt dieser Partition anzeigen. 

Zur Suche nach DBs in dieser Partition rekursiv durchsuchen lassen:\
fls -pr /dev/loop0p12 | grep "\\.db"

Wichtig: Sleuthkit kommt mit .wal nicht klar, dafür autopsy

dateien via inode extrahieren oder die Partition einfach mounten:\
`mount /dev/loop0p12 /mnt` 

DBs öffnen mit dem sqlite-browser. Gibt es keine Tables zur Auswahl, gibt es vermutlich Berechtigungsprobleme mit dem Verzeichnis. 

Möglicherweise relevant: Skype / SMS

-----------------

Exkurs YAFFS  / IoT

wenn yaffs nicht automatisch erkannt werden kann, eigene config

was erkennt yaffs? (drei ansätze gefordert) binwalk, sleuthkit, yaffshiv

----------------

Hier geht's weiter

Empfehlung binwalk 3.1.1 in Rust, zu finden auf 4n6

`cat /proc/filesystems` - welche Dateisysteme werden vom eigenen OS unterstützt

`modprobe qnx6` -> qnx6 als FS verfügbar machen

Koordinaten auf einer Karte anzeigen:\

`sqlite3 -header -separator " " DBNAME.db "select latitude, longitude from trips;" > out.csv`

Karte daraus bauen lassen;
```
1. Navigate to **Google My Maps** and select **Create a new map**.
    
2. Click **Import** under the default layer.
    
3. Upload your **CSV**, **XLSX**, or **Google Sheets** file.
    
4. Select the columns for **Latitude** and **Longitude** (or addresses) to position markers, and choose a column for marker titles.
    
5. Google Maps will automatically generate markers for each row, allowing up to **2,000 rows** per layer.
```

Bei der Suche nach multimediadateien nicht nach jpg etc greppen, sondern "image" im header der Datei

------------

### TWRP installieren und via `adb` sichern

Gerätename: Initialen der beiden Leute, die die Aufgabe zusammen machen

Zuerst ADB aktivieren

`adb devices` bis "device" statt "unauthorized".

`adb shell`  -> `uid=2000`

`adb reboot recovery` -> reboot ins recovery

Für TWRP wollen wir aber `adb reboot download`

Images gibt's von hpm, Datenträger mitbringen (32GB)

`heimdall detect` -> `Device detected`

`heimdall flash --RECOVERY twrp-3.2.1-0-i9300.img`  (--no-reboot bei einigen Smartphones nötig, S3 nicht)

`adb reboot recovery` -> TWRP lädt

`adb shell` , dann `cat /proc/partitions` zeigt alle Partitionen an, Pfad allerdings via\
`mount`

Dann via `adb pull /dev/block/mmcblk0 flash.img` zum sichern des gesamten Speichers

`mmls flash.img` -> zeigt alle Partitionen, die nun im Image vorhanden sind

`fls -f list` zeigt unterstützte Filesystems


#### Zurückflashen

`adb reboot download` 

hpm hat ein script;

```shell
heimdall flash --CACHE cache.img --BOOT boot.img --SYSTEM system.img --RECOVERY recovery.img --RADIO modem.bin --HIDDEN hidden.img --BOOTLOADER sboot.bin --TZSW tz.img
```

Danach `adb reboot recovery`, dort "Wipe Cache" und "Wipe Data", reboot -> Factory reset