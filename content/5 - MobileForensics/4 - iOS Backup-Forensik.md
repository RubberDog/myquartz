
#### iCloud-Backup
Bei iCloud-Daten sind gesetzliche Vorschriften zu beachten.\
Nur unter bestimmten Voraussetzungen darf auf diese Datensicherung zugegriffen werden.\
Bei iCloud-Backups gibt es verschiedene Optionen und Funktionen für eine individuelle Auswahl des Sicherungsumfangs.

Es ist zu beachten, dass dem Benutzer verschiedene Optionen beim Verlust des Gerätes zur Verfügung stehen, wie die Sperrung oder gar Löschung des Gerätes.

Zur Sicherung des iCloud-Backup werden die Apple-ID sowie das Passwort benötigt.\
Nach der Anmeldung können einzelne Bereiche wie z.B. Fotos heruntergeladen werden.

Oxygen Forensic Detective oder der UFED PA können Cloud-Sicherungen durchführen.

#### Elcomsoft Phone Password Breaker

Mit diesem Tool kann ein komplettes iCloud-Backup heruntergeladen und entschlüsselt werden.\
Ebenso hat man die Möglichkeit auch nur einzelne Bereiche auszuwählen, was den Prozess beschleunigt.\
Nach der Anmeldung mit den Accountdaten werden alle der Apple-ID zugeordneten iCloud-Backups angezeigt und können einzeln, oder nur Teilbereiche dieser, heruntergeladen werden.\
Liegen die Anmeldeinformationen nicht vor, jedoch das zugehörige Gerät und wurde das "iCloud Control Panel" zum erstellen von Backups genutzt, kann EPPB (Elcomsoft Phone Password Breaker) mit dem Tool ATEX genutzt werden, um ein Apple-Token zu extrahieren und dadurch Zugriff zu erlangen. Jedoch muss hierfür das jeweilige Gerätepasswort des Nutzers bekannt sein.


#### iTunes-Backup

Auf einem Computer, der mit dem iPhone verbunden war, können via iTunes Backups erstellt werden - diese Backups können auf dem Computer weiterhin vorhanden sein, weswegen eine Analyse sinnvoll ist. Diese Backups können schließlich auch Daten enthalten, die mittlerweile durch den Benutzer auf dem Gerät gelöscht wurden.\
Beim ersten Backup wird eine vollständige Sicherung des Gerätes erstellt, bei allen weiteren lediglich ein inkrementelles Backup - es sind also nur modifizierte Daten enthalten.

Im Backup sollte der volle Zugriff auf das Dateisystem der Datenpartition gewährt werden.\
Zwar lesen die meisten forensischen Tools die enthaltenen Datenbanken aus, jedoch liest keines alle Datenbanken im vollen Umfang aus, so dass meist eine manuelle Auswertung nötig ist.\
Gelöschte Daten können nur über eine manuelle Auswertung im Hex-Text erlangt werden.

Besonders relevante Dateien im Backup sind:
- info.plist
- manifest.mbdb
- manifest.plist
- status.plist

info.plist enthält Informationen zum Gerät, z.B. Gerätekennung, installierte Apps, etc\
manifest.plist zeigt an, ob das Backup verschlüsselt ist\
manifest.mbdb enthält eine Liste aller im Backup gespeicherten Daten - Beispiel zum Auslesen unter [[6 - Python-Beispiele#manifest.mbdb|Python-Beispiele]]

Selbst wenn das Backup verschlüsselt ist können diese Daten ausgelesen werden.


#### Verschlüsselte Backups

Während der Sicherung kann via iTunes ein Passwort für das Backup festgelegt werden.\
Bei weiteren Sicherungen wird dies nicht abgefragt, jedoch bei der Wiederherstellung von Daten durch dieses Backup.

Hier wird wieder [[#Elcomsoft Phone Password Breaker]] erwähnt, damit kann man das Passwort erraten oder einen Bruteforce starten.

Benutzung:\
- EPPB starten und "Password Recovery Wizard" auswählen
- Quelle "iOS device Backup" wählen
- Backup-Datei und zugehörige manifest.plist auswählen
- Konfigurieren des BF und "Start" klicken
- Bei Erfolg wird das Passwort im Hauptmenü angezeigt.