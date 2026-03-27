fls wird genutzt, um Dateien und Ordner in einem Image anzeigen zu können.

Hier ein Beispielaufruf, um Dateien mit "SAM" im Dateinamen in einem gemounteten loop-Device zu finden;

`fls -pr /dev/loop0p2 | grep -i SAM$` 

`-pr`: "p" zeigt den vollen Pfad jedes gefundenen Eintrags, "r" lässt das Image rekursiv durchsuchen.

`/dev/loop0p2` ist die Partition2 des loop-device0 und gibt den Ort des Images an

`grep` kennen wir schon, es filtert die Ausgabe nach dem Suchbegriff

`-i` ignoriert den Case (Groß- / Kleinschreibung)

`SAM$` besagt, dass der Suchbegriff SAM lautet, durch das `$` ist festgelegt, dass der Datei- / Ordnername mit SAM endet.

Die Ausgabe kann dann sein;

![[Pasted image 20260326110250.png]]

Die markierte Zahl stellt die Nummer des inode da, welchen wir in der Folge für [[istat]] oder [[icat]] benötigen.

Gleiches funktioniert auch für die Registry-Hives System und Software via\
`fls -pr /dev/loop0p2 | grep SYSTEM$` und \
`fls -pr /dev/loop0p2 | grep SOFTWARE$`

Ganz wichtig auch die `NTUSER.DAT$` - aufpassen! Diese Datei gibt's für jeden einzelnen Nutzer!

-----

Timeline erstellen;

`fls -pr -m "c:" /dev/loop0p2 > bodyfile`

`fls -pr` wurde oben schon erklärt.\
`-m "mountpoint"` gibt einen Mountpoint an, der fls in der Pfadangabe als "Anfang" dient.\
Bei Windows wäre dies z.B. "c:", wenn es sich bei dem Image um das C-Laufwerk handelt. Unter Linux könnte es beispielsweise direkt "/", das root-Verzeichnis sein, oder aber "/home/", oder was auch immer. Das sollte man vorher feststellen.\
`/dev/loop0p2` ist das Image im loop-Device, welches durch fls betrachtet werden soll.\
Zuletzt dann `> bodyfile`, um es in eine Datei "bodyfile" im aktuellen Verzeichnis zu schreiben.