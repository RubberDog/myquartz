
#### Zeitstempel

Timestamps werden entweder im Unix- oder Max absolute time Format gespeichert.\
Bei der Analyse von Apps kann das WebKit/Chrome time Format hinzukommen.

Wichtig: manuell in Datenbanken verifizieren.\
Alle Timestamps können mit dem kostenlosen Tool [DCode](https://www.digital-detective.net/dcode/) konvertiert werden.


#### SQLite-Datenbanken

Smartphones speichern große Teile der Daten in SQLite-Datenbanken, darunter z.B.:
- E-Mail-Daten
- Addressbuch-Kontakte
- SMS

Auch Apps wie Facebook, WhatsApp, etc. pp nutzen SQLite-Datenbanken, die Dateiendungen sind meist `.db` oder `.sqlitedb`.\
Als Tool zum auslesen bietet sich der [DB Browser for SQLite](https://github.com/sqlitebrowser/sqlitebrowser/releases) an.

Bei den meisten kommerziellen Tools ist ein SQLite-Browser bereits integriert.


#### Temporäre Dateien

Hier sind damit `.wal`-Dateien (**W**rite **A**head **L**ogs) und Journal-Files gemeint.\
Journal-Dateien speichern Originaldaten vor einer Transaktionsänderung, damit bei einem Fehler die Datenbank in den ursprungszustand zurückversetzt werden kann.

WAL-Dateien hingegen speichern aktuelle Änderungen in der Datenbank und wenden diese nach einer festen Zeit oder einer bestimmten Anzahl vorzunehmender Änderungen auf die eigentliche Datenbank an.

Hint (über das Script hinaus): Vorsicht bei der Nutzung von Sicherungen mit WAL-Dateien. Je nach Tool werden die darin vorhandenen Änderungen beim öffnen auf die Datenbank angewandt. Der Zustand der Original-DB kann dadurch verloren gehen.


#### Wichtige iOS-Datenbanken

Eine Übersicht, die 1:1 übernommen wurde:

| Datenbank (Pfad)                                          | Datenbankinhalt                   |
| --------------------------------------------------------- | --------------------------------- |
| /Library/CallHistory/call_history.db                      | Anruflisten                       |
| /Library/CallHistoryDB/CallHistory.storedata              | Anrufprotokoll                    |
| /Library/AddressBook/AddressBook.sqlitedb                 | Kontakte                          |
| /Library/AddressBook/AddressBookImages.sqlitedb           | Kontaktbilder                     |
| /Library/SMS/sms.db                                       | SMS Mitteilungen                  |
| /Library/SMS/Attachments/                                 | MMS Dateien                       |
| /Library/Calendar/Calendar.sqlitedb                       | Kalender                          |
| /Library/Calendar/Extras.db                               | Kalender Extras                   |
| /Library/Notes/notes.sqlite                               | Notizen                           |
| /Library/Safari/                                          | Safari Aktivitäten                |
| /com.apple.mobilesafari/Library                           | Safari Aktivitäten                |
| /Library/Accounts/Accounts3.sqlite                        | Benutzerkonten                    |
| /Library/Caches/com.apple.WebAppCache/ApplicationCache.db | Web Cache                         |
| /Library/Keyboard/UserDictionary.sqlite                   | Benutzerdefinierte Auto-Korrektur |
| /Library/Voicemail/voicemail.db                           | Voicemail                         |
| /Library/Databases/CellularUsage.db                       | Zuletzt verwendete SIM Karten     |
| /Library/TCC/TCC.db                                       | Applikationsrechte                |
| /Library/BatteryLife/CurrentPowerLog.PLSQL                | Batterie Lebenszeit-Tracker       |


#### SQLite-Datenbanken manuell auslesen

In diesem Abschnitt steht eigentlich nur, dass es mit SQLite-Queries und dem bereits genannten [DB Browser for SQLite](https://github.com/sqlitebrowser/sqlitebrowser/releases) erfolgen sollte und man sich nicht darauf verlassen kann, dass automatisierte Tools alle Datenbanken vollständig und korrekt auslesen.


#### SQLite-Datenbanken und Timestamps

Auch in DBs können Timestamps gespeichert werden, sie können wie folgt konvertiert werden:

Unix Epoch ist Sekunden seit dem 01.01.1970 00:00:00

Unix Epoch (10-stellig) in UTC: \
`SELECT datetime(TS_COLUMN,'unixepoch')`\
in localtime:\
`SELECT datetime(TS_COLUMN,'unixepoch', 'localtime')`


Unix Epoch Milliseconds (13-stellig) in UTC:\
`SELECT datetime(TS_COLUMN/1000,'unixepoch');`


Hingegen die Mac absolute time in Sekunden seit dem 01.01.2001 00:00:00

Um diese korrekt zu konvertieren muss vorher die Anzahl der Sekunden seit Unix Epoch (bis eben Mac absolute time) addiert werden:\
`SELECT datetime(TS_COLUMN+978307200, 'unixepoch');`


Der Chrome-Timestamp stellt die Zeit in Mikrosekunden dar und muss deswegen vor der konvertiertung durch 1.000.000 geteilt werden;\
`SELECT datetime(TS_COLUMN/1000000 + (strftime('%s','1601-01-01')),'UNIXEPOCH');`

#### Property-List (plist)

PLists sind strukturierte Textdateien ähnlich .xml, die als ASCII oder Binär vorliegen können.

Ausgelesen werden sie je nach Format mit einem simplen Texteditor oder einem PList-Viewer wie z.B. [plutil](https://github.com/withgraphite/plutil).


Eine Tabelle relevanter PList-Dateien, 1:1 übernommen:

| PList                                                                                  | PList Beschreibung                                                                                      |
| -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| info.plist                                                                             | iOS Geräteinformationen (Telefonnummern, iOS Version usw.)                                              |
| status.plist                                                                           | Letzte Sicherung und weitere Daten                                                                      |
| manifest.plist                                                                         | Verschlüsselungsstatus                                                                                  |
| /private/var/mobile/Library/Preferences/com.apple.homesharing.plist                    | iCloud Benutzerkontoeinstellungen                                                                       |
| /private/var/mobile/Library/Preferences/com.apple.assistant.backedup.plist             | Cloud Synchronisationseinstellungen                                                                     |
| /private/var/mobile/Library/Preferences/com.apple.coreduetd.plist                      | Synchronisationsgeräte                                                                                  |
| /private/var/mobile/Library/Preferences/com.apple.mobilephone.plist                    | zuletzt eingegebene Rufnummer, unabhängig davon, ob diese tatsächlich gewählt wurde oder nicht          |
| /private/var/mobile/Library/Preferences/com.apple.mobilephone.speeddial.plist          | Liste der hinzugefügten Kontakte                                                                        |
| /private/var/mobile/Library/Preferences/com.apple.accountsettings.plist                | Liste der E-Mail Konten                                                                                 |
| /private/var/mobile/Library/Preferences/com.apple.Maps.plist                           | letzter Breitengrad, Längengrad und die letzte Adresse, die in der Karten Applikation festgelegt wurden |
| /private/var/mobile/Library/Preferences/com.apple.mobilemail                           | Abrufdaten E-Mails und verwendete E-Mail-Signaturen                                                     |
| /private/var/mobile/Library/Preferences/com.apple.Preferences.plist                    | Tastatursprache, die zuletzt auf dem Gerät verwendet wurde                                              |
| /private/var/mobile/Library/Preferences/com.apple.mobilesafari.plist                   | Zuletzt durchgeführte Suchanfragen (Safari)                                                             |
| /private/var/mobile/Library/Safari/History.plist                                       | Safari Browserverlauf                                                                                   |
| /private/var/mobile/Library/Safari/SuspendState.plist                                  | Titel der Webseite und die URL aller gesperrten Webseiten auf Safari                                    |
| /private/var/mobile/Library/Preferences/com.apple.springboard                          | Applikationen, die entsprechend der iOS Version angezeigt werden                                        |
| /private/var/mobile/Library/Preferences/com.apple.mobiletimer.plist                    | aktuelle Zeitzone, Timer, Alarme und Stoppuhren                                                         |
| /private/var/mobile/Library/Preferences/com.apple.weather.plist                        | Städte für Wetterberichte; Datum und Uhrzeit der letzten Aktualisierung                                 |
| /private/var/mobile/Library/Preferences/com.apple.preferences.network.plist            | Status von Bluetooth und Wi-Fi Netzwerken                                                               |
| /private/var/mobile/Library/Preferences/com.apple.conference.plist                     | Facetime-Telefonnummer, SMS-Telefonnummer, Benutzerkonten                                               |
| /private/var/mobile/Library/Preferences/com.apple.conference.history.plist             | Telefonnummernhistorie und Benutzerkontendaten, die zur Kommunikation via Facetime genutzt wurden       |
| /private/var/mobile/Library/Preferences/com.apple.identityservices.idstatuscache.plist | iCloud Synchronisation, Email, Facetime usw.                                                            |
| /private/var/mobile/Library/Maps/Bookmarks.plist                                       | Bookmarks für Standorte in der Maps Applikation                                                         |
| /private/var/mobile/Library/Caches/com.apple.mobile                                    | Liste aller System- und Benutzeranwendungen inklusive Pfadangaben                                       |
| /private/var/root/Library/Preferences/com.apple.preferences.network.plist              | Informationen, ob der Flugmodus derzeit aktiviert ist oder nicht                                        |
| /private/var/root/Library/Lockdown/pair_records                                        | Ordner mit Privatschlüsseln, die zum Koppeln des Geräts mit einem Computer genutzt werden               |
| /private/var/root/Library/Caches/locationd/clients.plist                               | Standortvorgaben für Applikationen und Systemdienste                                                    |
| /private/var/preferences/SystemConfiguration/com.apple.network.identification.plist    | Netzwerkinformationen der gecachten IP                                                                  |
| /private/var/preferences/SystemConfiguration/com.apple.wifi.plist                      | bekannten Wi-Fi-Netzwerke und letzte Verbindungen                                                       |


#### Weitere relevante Daten

Natürlich gibt es auch relevante Daten, die nicht in diesen DBs zu finden sind - darunter
- Cookies
- Fotos
- Videos
- Apps
- Tastatur-Cache

Eine Tabelle weiterer, relevanter Datei-Locations - 1:1 übernommene Tabelle:

|Relevante Dateien|Beschreibung|
|---|---|
|/Library/Preferences|Einstellungen (PLists)|
|/Library/DataAccess|Benutzerkontoinformationen, welche für die Einrichtung von Applikationen verwendet werden|
|/Library/DeviceRegistry/|Apple Watch|
|/Library/Keyboard|dynamic-text.dat|
|/DCIM/1*APPLE Folder|Vom Benutzer erstellte bzw. gespeicherte Lichtbilder|
|/Media/PhotoData|Fotos, die aus Live-Video und SMS-Fotoerfassung gespeichert wurden|
|/Applications|Applikationsordner|
|/Library/Cookies/Cookies.binarycookies|Safari Aktivität|
|/Library/Preferences/com.apple.assistant|Siri|
|/Library/Preferences/com.apple.imservice|SMS, iMessage und Facetime|
|/Media/Recordings|Sprachnotizen|
|/Library/Voicemail|Sprachnachrichten|
|/Library/Notes/notes.idx|Notizen|

Bei `cookies.binarycookies` handelt es sich um eine Binärdatei, dem nachfolgenden Script übergibt man den Pfad zum Cookie und erhält alle darin gespeicherten Daten.\
Zu finden ist das Script auf [GitHub](https://github.com/mfpp/BinaryCookieReader).

`dynamic-text.dat` findet sich unter `/private/var/mobile/Library/Keyboard` und enthält im Schnitt 600 vom Nutzer eingegebene Wörter. Auch hier handelt es sich um eine Binärdatei, die mit einem HexViewer gelesen werden kann.

Mit dem Gerät selbst aufgenommene Fotos finden sich in `/private/var/mobile/Media/DCIM`, ebenso Screenshots und thumbnails dieser Bilder.\
Diese enthalten üblicherweise auch EXIF-Daten wie die Aufnahmezeit und manchmal die Geolocation, welche z.B. mittels [ExifTool](https://exiftool.org/) ausgelesen werden können.

Für jede vom Nutzer installierte App wird ein Verzeichnis im Pfad `/private/var/mobile/Applications` angelegt, wo die Apps PLists, Datenbanken etc. abspeichern und wie zuvor erklärt betrachtet werden können.\
Teilweise werden diese Daten verschlüsselt gespeichert, was eine Analyse erschwert.


#### Wiederherstellung gelöschter SQLite-Datenbankeinträge

Da forensische Tools nicht unbedingt alle gelöschten Datenbankeinträge finden und wiederherstellen kann eine manuelle Betrachtung mittels Hexeditor nötig sein.

Das SQLite Format 3 ist nach wie vor aktuell, dessen Header lautet:\
```hex
53 51 4c 69 74 65 20 66 6F 72 6D 61 74 20 33
```

Ein Script zum Wiederherstellen - da dies manuell extrem zeitaufwändig sein kann - findet sich erneut auf [GitHub](https://github.com/mdegrazia/SQLite-Deleted-Records-Parser/releases), die Benutzung ist [hier](https://github.com/mdegrazia/SQLite-Deleted-Records-Parser#sqlite-parser) erklärt.