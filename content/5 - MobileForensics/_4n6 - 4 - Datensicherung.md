
### Ein SDK Gastsystem sichern

Im großen und ganzen steht hier nur, dass virtuelle Smartphones im User-Verzeichnis ( hier /home/hpm) im Unterzeichnis `.android/avd/` abgelegt werden.

Die Image-Dateien
- sdcard.img (Image einer virtuellen SD-Karte, kann direkt gemountet werden)
- userdata.img (Image-Template vor der Nutzung, im wipe-Zustand)
- userdata-qemu.img (Image in Gebrauch mit allen Apps und Daten)

Diese Dateien liegen als physische Images vor. Handelt es sich um gängige Dateisysteme wie ext4, so können sie direkt gemountet werden - z.B. mit Sleuthkit:
```shell
mount -o ro,noatime,noexec sdcard.img /mnt
umount /mnt
mount -o ro,noatime,noexec userdata-qemu.img /mnt
```


### Logische Sicherung

Drei Übungsaufgaben  :) 


### Physische Sicherung

Das Gerät muss hierzu gerootet sein und ADB muss aktiv sein. Bei älteren Geräten ist das mit TWRP möglich.

##### SDK mit ext4
Hier wird ein virtuelles Smartphone (in Android Studio) als Asservat genutzt.\
Um eine Physische Sicherung zu erhalten, müssen root-rechte vorhanden und ADB aktiv sein. Beides ist in den virtuellen Geräten gegeben.

Für die **dd / netcat**-Variante muss ein Listener vorhanden sein, dieser wird gestartet mittels `nc -l -p 8888` **oder**  `nc -l 8888`.\
Je nach im System vorhandener Version von netcat kann der Port einfach so angegeben werden, oder muss mit der Option `-p` übergeben werden.

*Hier hört diese Variante auch schon auf. Blödes Script. Laut Internet geht's wie folgt weiter;*

`nc -l -p 8888 > image.dd` wird auf dem Sicherungs-PC gestartet, um alle Daten die an Port 8888 ankommen in die Datei `image.dd` zu schreiben.

Auf der Smartphone-Seite wird dann

`dd if/dev/block/mmcblk0 bs=4096 | nc <HOST-IP> 8888` ausgeführt. Dann dauert's.

Großes Problem dabei; Gibt es hier Verbindungsabbrüche, ist die Sicherung hinüber. Es kann nicht wieder aufgenommen werden, man muss neu anfangen.

**adb pull**-Variante\
Auf dem Host-PC `adb pull /dev/block/mmcblk0 > image.dd` - fertig. Hab' ich tatsächlich schonmal so gemacht. Funktioniert super.


#### Image auf SD-Karte (YAFFS)

Hier werden ein paar Befehle genannt, das große Problem; das genannte Programm `nanddump` ist hier auf der Website nicht zu finden.. naja. Die Befehle wären;

```shell
adb shell mount # zeigt die gemounteten Partitionen
adb shell cat /proc/mtd # zeigt die Größen und Namen der Partitionen 
adb push nanddump /data/local/tmp # pushed "nanddump" nach tmp
adb shell

cd /data/local/tmp
-/nanddump -f /mnt/sdcard/data.nanddump /dev/mtd/mtd9ro
```

**WARNUNG**\
Was leider nicht so direkt erkennbar ist;\
Hier wird das Image auf die SD-Karte geschrieben - wenn man also keine leere eingelegt hat, überschreibt man ggfs. die Daten des Besitzers... die man ja eigentlich haben will.


#### Image per ADB (YAFFS)

Hier ist der Ablauf sehr ähnlich, aber zusätzlich wird netcat genutzt;

```shell
adb shell mount # zeigt die gemounteten Partitionen
adb shell cat /proc/mtd # zeigt die Größen und Namen der Partitionen 
adb push nanddump /data/local/tmp # pushed "nanddump" nach tmp
adb push nc /data/local/tmp # pushed auch netcat ("nc") nach tmp
adb forward tcp:8888 tcp:8888 # baut einen tcp-Kanal zwischen Host und Smartphone auf
adb shell
cd /data/local/tmp
./nanddump /dev/mtd/mtd9ro | ./nc -l -p 8888 # dumped die Daten und stellt sie über nc bereit

# Auf dem Host ausführen:
nc 127.0.0.1 8888 > data.nanddump
```


#### Image auf SD-Karte (ext4)

Könnte kaum einfacher sein:

`adb shell mount` um die Partitionen zu sehen, in diesem Fall `system` heraussuchen und auf eine eingelegt, leere SD-Karte schreiben;

```shell
adb shell
dd if=/dev/block/mmcblk0p9 of=/mnt/extSdCard/system.dd
```


#### Image per ADB (ext4)

```shell
adb shell mount
adb push nc /data/local/tmp
adb forward tcp:8888 tcp:8888
adb shell
cd /data/local/tmp
dd if/dev/block/mmcblk0p9 | nc -l -p 8888
exit
nc 127.0.0.1 8888 > system.dd
```

`dd` und via netcat pipen und einsammeln genauso für `/data` und `/cache`.


#### Die pull-Variante

Verweis auf das Webinar.

Sollte tatsächlich nur 

```shell
adb shell mount
adb pull /dev/block/mmcblk0 > flash.dd 
```
sein um den gesamten Flash-Speicher zu ziehen. Für einzelne Partitionen entsprechend mit `p<NUMMER>` und dem dd-Namen anpassen.


### File Carving

Gelöschte Dateien wiederherstellen nennt sich "Carving". Er hat den falschen Wiki-Artikel eingebunden, dort geht's um Skifahren.... Korrekt ist [der hier](https://de.wikipedia.org/wiki/Carving_(Datenrettung))

Die Seite "Übung" ist leer und "Foremost" ist auch nur n Wiki-Artikel. Ist wohl noch SEHR "Work in Progress", der Teil..