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