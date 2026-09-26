Für die Prüfung - bzw den Teil vor Ort - wird ein Laptop mit ADB (Android Debug Bridge) und Heimdall empfohlen.

- ADB für Windows gibt's [hier](https://www.chip.de/downloads/Minimal-ADB-and-Fastboot_62500183.html)
- für Linux als Paket "ADB" in den Repositories, z.b. `sudo apt install adb`
- für Mac über homebrew via `brew install android-platform-tools`

Zur Nutzung werden zuerst im Smartphone die Entwickleroptionen aktiviert (Build-Nummer in den Einstellungen suchen, 7x antippen), danach in den Entwickleroptionen "USB Debugging" aktivieren.

Mittels `adb devices` nachschauen, ob das Gerät erkannt wird. (ID-Nummer + "device" sollte in der Zeile stehen).\
Steht dort "authenticating", so muss auf dem Gerät die Verbindung bestätigt werden (Pop-Up erscheint im Display). Ist das nicht möglich, Gerät neu Verbinden, Pop-Up sollte auftauchen.

`adb shell` gibt Kommandozeilenzugriff.

`id` gibt den aktuellen Benutzer aus, vermutlich `uid=2000(shell)`. Ist das Gerät nicht gerootet, kann `su`nicht ausgeführt werden.


### Download-Modus

Um z.B. TWRP zu installieren, will man in den Download-Modus; `adb reboot download`.

Der Download-Modus ist auch erreichbar über die Tastenkombination "Volume Down + Home + Power", bei neueren Geräten meist "Volume up + Power" - " Volume down + Power" ist meistens ein erzwungener reboot.

Nur am Rande interessant, weil nicht für das Modul relevant; 
- Bei halbwegs aktuellen Geräten muss meistens ein USB-Kabel angeschlossen sein, um den Download-Modus aufrufen zu können
- seit kurzem ist bei Samsung der Download-Modus nahezu nicht mehr existent.


### Recovery-Modus

Hat man adb-Zugriff, dann ist dieser Modus über `adb reboot recovery` erreichbar.\
Die Tastenkombination mit gleichem Ergebnis ist "Volume up + Home + Power".

Der normale Recovery-Modus bietet üblicherweise keinen Zugriff via ADB.\
Läuft dort jedoch TWRP als Recovery, so hat man adb-Zugriff mit vollen Root-Rechten auf das Gerät.


### Apps via ADB installieren

Hat man eine App - also .apk-Datei - und möchte sie ohne den Playstore installieren, kann dies via SD-Karte oder ADB passieren. Hierzu muss allerdings in den Entwickler-Optionen "Apps per USB überprüfen" angehakt sein.


### Liste installierter Apps

`adb shell 'pm list packages -f' | sed -e 's/.*=//' | sort`


### adb push / pull 

Dieser Befehl ist auch für den Präsenztag relevant.

Um wie zuvor eine App-Liste zu erstellen und sie lokal auf dem Telefon zu speichern, wird nach dem Verbinden via shell ( `adb shell` ) folgender Befehl genutzt:\
`pm list packages > /data/local/tmp/applist.txt`

Damit wird die Liste im tmp-Verzeichnis gespeichert, worauf jeder User Zugriff hat.\
Mittels `exit` wird zunächst die adb-Shell verlassen.\
Danach kann mittels `adb pull /data/local/tmp/applist.txt` diese Liste vom Smartphone in das aktuelle Verzeichnis des Host-Computers gezogen werden.

`adb push` macht es genau anders herum und schiebt Dateien vom Host-Computer auf das Smartphone, hier am Beispiel einer simulierten Malware.

Damit das funktioniert, muss sie für die ARM-Architektur kompiliert sein. das kann mittels "file"-Programm überprüft werden

![[Pasted image 20260926120951.png]]

Mittels `adb push /tmp/nc /data/local/tmp` kann die Datei auf das Smartphone kopiert werden.

Um sie zu starten, verbindet man sich zuerst mittels `adb shell` wieder mit dem Smartphone und ruft dann die Datei auf: `/data/local/tmp/nc`.

![[Pasted image 20260926121133.png]]