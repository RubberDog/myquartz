Mittels icat können Daten aus einer Datei gelesen und Beispielsweise der Ausgabestrom in eine neue Datei umgeleitet werden.
Es handelt sich dabei um das Programm `cat`, jedoch wird hier eine inode anstelle eines Dateinamens als Input erwartet.

Ein Beispielaufruf wäre
`icat /dev/loop0p2 59953 > /tmp/SAM`
Damit wird der Inhalt der Datei, auf welche der inode 59953 im Image des loop-Device0, Partition2, in eine (neue) Datei unter `/tmp/SAM` geschrieben.
