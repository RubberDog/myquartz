
#### **Alte Infos - Stand ~ 2018**

Beginnend mit dem feststellen des exakten Modells sowie der iOS-Version;

Modell via;
- Einstellungen -> Allgemein -> Info -> Modell 
Softwareversion via;
- Einstellungen -> Allgemein -> Info -> Version

Nicht weiter wichtig, da wir eh maximal ein Image bekommen.

CLI;
Hier bietet sich ideviceinfo aus [libidevicemobile](https://github.com/libimobiledevice/libimobiledevice/tree/master) an.

### FileSystem

Es gibt zwei Partitionen, einmal für das System und einmal für UserData.\
System ist r/o, Jailbreaking entfernt den Schreibschutz, wodurch Third-Party-Applications installiert werden können.

UserData enthält alle Nutzergenerierten Daten und ist unter `/private/var` zu erreichen.\
Darin finden sich Beispielsweise:
- Anruflisten und SMS
- E-Mails und Chats
- Passwörter (Accounts, Web-Accounts, WLAN)
- Browserverlauf
- Dokumente, Settings, DBs
- Bilder / Videos
- Geolocations, Routen, Orte
- Diverse Logfiles