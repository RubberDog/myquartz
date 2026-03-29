Zuerst erstellen wir ein Verzeichnis, in welches dann die Shadow-Kopie gemountet wird;\
`sudo mkdir /vss`, danach\
`vshadowmount /dev/loop0p2 /vss`

Schaut man danach in `/vss` nach, so finden sich - in dem Vorlesungs-Beispiel - dann 5 Shadow-Kopien. Dabei handelt es sich um Partitionen, weswegen [[mmls]] leider keine Infos zeigt.\
`fsstat /vss5` hingegen zeigt uns die Informationen zum Filesystem des VSS5;\
![[Pasted image 20260329160331.png]]

Mit `fls vss5` können wir ins Dateisystem hineinschauen. Sind dort Sternchen in jeweiligen Zeilen der Dateinamen, so handelt es sich um gelöschte Dateien;\
![[Pasted image 20260329160507.png]]

Dies beweist übrigens auch, dass es sich um eine physische Kopie des Laufwerks handelt - bei eine logischen Sicherung wären nur aktuell vorhandene Dateien auffindbar.

Hintergrund;\
Beim Löschen einer Datei bleiben die Daten auf der Festplatte vorhanden, sie werden nicht überschrieben. Es wird jedoch der Verzeichniseintrag entfernt (im Mastefiletable, das hatten wir mal in "Betriebssysteme") und der inode, sowie die zugehörigen Speicherblöcke als "frei" markiert, jedoch nicht sofort überschrieben. Die Daten sind also noch da, ohne weitere Informationen (Beginn und Ende des Speicherplatzes) weiß das Betriebssystem jedoch nicht, dass es sich hierbei um zusammenhängende Daten, also eine verwertbare Datei handelt.\
Detail am Rande: Sleuthkit (und wir hier) nennen es inode, Windows kennt das Prinzip eines inode aber gar nicht. Dort ist es ein Verzeichniseintrag im Masterfiletable.\
inode ist hier als abstraktes Konzept zu verstehen und meint den Metadaten-Eintrag im jeweiligen Dateissystem.

Haben wir dann z.B. mittels [[fls]] und dem Befehl\
`fls -pr vss5 | grep -i "\.pst$"`\
eine passende Outlook-Datei gefunden, können wir diese mittels [[icat]] wie gewohnt wiederherstellen.

Weiter geht's dann in [[readpst]].