regripper ist in keiner der VMs vorinstalliert.\
Es kann aber einfach aus den Repositories installiert werden, in der 4n6-VM mittels\
`sudo apt install regripper`

Die vorhandenen Plugins können mittels\
`regripper -l`\
angezeigt werden.\
Es sind allerdings 249 verschiedene Plugins vorinstalliert - mittels `grep` kann aber gefiltert werden. Davon ausgehend, dass man nicht immer das genaue Suchwort im Plugin-Namen kennt bietet sich folgender Befehl an:\
`regripper -l | grep -1 -i win`

- `regripper -l` listet die Plugins
- `grep` ist soweit bekannt
-  die Option `-1` sorgt für die Ausgabe der Zeile vor und nach dem Treffer - falls man das Wort in der Beschreibung, nicht aber im Plugin-Namen trifft
- die Option `-i` ignoriert lower- / uppercase
- `win` ist das gesuchte Wort.

Beispielhafter Aufruf für Betriebssystem-Informationen:\
`regripper -p winver -r SOFTWARE`

 `-p winver` benennt das von regripper zu nutzende Plugin\
 `-r SOFTWARE` den zuvor mittels [[icat]] extrahierten Registry-Hive SOFTWARE

-----------

Netzwerk-Informationen über das Plugin `nic2` im System-Hive;

![[Pasted image 20260327101620.png]]

---------------

Infos zum Plugin `usb`;\
Hier bekommt man die meisten Geräte angezeigt, jedoch nur in diesem Format:\
![[Pasted image 20260327100625.png]]

Andere USB-Plugins zeigen weniger an!\
Um jedoch Geräte Identifizieren zu können, bietet sich die manuelle Überprüfung auf https://www.devicehunt.com an.

Dort den "Type" auf USB ändern, die gefundene Vid (4-stellig) als Vendor-ID und die Pid (4-stellig) als Device-ID angeben, und man findet z.B.;\
![[Pasted image 20260327100913.png]]

-----------

`-p mountdev` gibt Informationen zu gemounteten Geräten an, z.B. auch der Laufwerksbuchstabe.\
![[Pasted image 20260327104316.png]]

Eine Zuordnung, um welches Gerät (Hersteller, Modell, etc) es sich handelt ist darüber aber nicht möglich.\
Es gibt nur Volume-IDs aus, die man im registry-Hive SYSTEM wohl irgendwo unter `Enum\SCSI` auflösen könnte - aber dafür konnte ich kein passendes Plugin finden, wäre also manuelle Nacharbeit mit dem Registry-Editor oder sowas nötig. 

-----------------
Eventuell hilft bei USB-Festplatten `-p wpdbusenum` - kann ich aktuell leider nicht verifizieren, jedoch soll es als "Windows Portable Device BUS Enumeration" prinzipiell genau dafür da sein.. im Dell-Image sind keine Daten zu externen USB-Festplatten.\
![[Pasted image 20260327105439.png]]