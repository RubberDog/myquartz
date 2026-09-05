
Einer der ersten Schritte soll immer sein, die Registry-Hives zu erhalten.
Diese finden sich auf der C:-Partition und heißen;

- SAM
- SOFTWARE
- SYSTEM
- NTUSER.DAT

Die drei Hives SAM / SOFTWARE / SYSTEM liegen alle in dem Verzeichnis `Windows/System32/config`, als Randnotiz; "system" ist im Dell-Image nicht uppercase geschrieben.\
Daher eher auf das Verzeichnis statt den exakten Dateinamen achten!

Detaillierteres und wie man sie erhält ist verteilt auf [[fls]], [[icat]] und [[regripper]].\
Alternativ zur "komplexen" herangehensweise, um die Dateien zu erhalten, können sie auch aus dem gemounteten Image einfach herauskopiert werden. Restliche Bearbeitung der Registry wäre dann nur noch mit [[regripper]].

-------

HPM erwartet IMMER Angaben zum vorliegenden Image, z.B. 

- das Betriebssystem in der .E01
- Servicepack
- Installationsdatum
- Benutzer (RegisteredOwner)

Diese Infos finden sich sehr einfach mittels [[regripper]].

Wenn eine Datei z.B. mittels [[icat]] aus einem Image extrahiert wurde, sollte man danach mittels
`file dateiname` prüfen, ob der Dateityp der Erwartung entspricht.\
In der [[VL 24.03.2026]] wurde dort z.B. das Dateiformat "MS Windows Registry File, NT/2000 or above" bzw "Microsoft Outlook Personal Storage" erwähnt.

Auch wenn dabei ein falsches Ergebnis herauskommt können so durch die Überprüfung noch Teil-Punkte gegeben werden!

--------------------

Wichtig in der APL für maximale Punkte;

- Immer den genutzten Befehl - im Text! - angeben.
- Immer einen Screenshot der erzeugten Ausgabe anfertigen
- Immer mit einem Satz abschließen, der alle relevanten Informationen enthält - vermutlich sucht er mit Strg-F oder einem Script den Text ab, Screenshots würden dabei nicht beachtet!
	- relevante Infos, z.B. zum Betriebssystem;
		- "Es handelt sich um ein Windows ZAHL mit Service-Pack ZAHL aufgesetzt am DATUM von Benutzer BENUTZERNAME"


----------------------

Microsoft kennzeichnet USB-HDDs nicht als USB-Geräte, sie werden als normale Festplatten genutzt / angezeigt.\
[[regripper]] hat angeblich Plugins zur Identifizierung - hier konnte ich aber bisher nur das Plugin `mountdev` (kurze erklärung in [[regripper]]) feststellen, was jedoch noch nicht so richtig hilft.
Alternativ klappt möglicherweise das Plugin `wpdbusenum` (Windows Portable Device BUS Enumeration), auf dem Dell3-Image war jedoch nichts vorhanden.

