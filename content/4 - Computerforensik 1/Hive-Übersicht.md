
SYSTEM
- USB-Geräte via `usbstor`, `usb` und `usbdevices`
- Festplatten (auch USB-HDD) via `mountdev` bzw `mountdev2` (letzteres empfohlen)
- Netzwerkinformationen via `nic2` und `networksetup2` (letzteres nicht in dell3)
- Zeitzonen-Einstellungen via `timezone`
- Dienste via `services`, z.B. "VSS" für [[vshadowinfo]], ggf. Tor (nicht in dell3)
- Ausführbare Dateien und letzte Modifikationszeit via `shimcache` 
	- weist nach, dass Datei X zu Zeitpunkt Y auf dem System vorhanden war
	- auch gelöschte Dateien können dort noch vermerkt sein
	- KEINE Garantie, dass die Datei auch ausgeführt wurde
- Hostname via `compname`


SOFTWARE
- Netzwerkinformationen
	- `networklist` vs. `networklist_tln` - letzteres stellt die gleichen Daten direkt als Timeline bereit  - nichts passendes in dell3
		- Gateway-MAC
		- Netzwerktyp (Kabel, WIFI)
		- Verbindungsdaten (erster / letzter Zeitpunkt)
	- `networkcards`
		- Netzwerkkarten-Name
		- MAC-Adresse
		- Zeitpunkt der letzten Verwendung
- Installationszeitpunkte (nicht unbedingt vollständig!) von Programmen via `installer`


SAM
- `samparse` zeigt die vorhandenen Benutzer und deren Berechtigungen.
	- Gruppen mit kurzen User-IDs (z.B. S-1-5-11) die ihnen zugeordnet sind, sind "Systemidentitäten" und können ignoriert werden. Sollten neben den kurzen jedoch auch lange User-IDs (z.B. S-1-5-21-2000478354-688789844-1708537768-501) ist das (mehr oder weniger) ungewöhnlich und sollte dokumentiert werden, wie beispielsweise in der Gruppe "Administrators".


NTUSER.DAT
- Zuletzt geöffnete Dateien / Ordner, sortiert nach Typ, via `recentdocs`
- Installierte Software via `listsoft` - nach den Einträgen Googlen, ist nicht immer offensichtlich
- Welche Programme wann und wie oft ausgeführt wurden via `userassist`
	- WICHTIG: Unter "Value names with no timestamps" sind (in dell3) einige "unlesbare" Einträge - die sind Rot13-"Verschlüsselt". [Cyberchef](https://gchq.github.io/CyberChef/) mit "Encryption/Encoding" -> ROT13 hilft weiter.
- Manuell über "Run Command" (Windows + R) eingegebene Befehle via `runmru` 
- Wurde "Putty" für SSH genutzt, können gespeicherte Hostkeys über `putty` ausgelesen werden