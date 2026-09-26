
In diesem Kapitel ist nur ein Abschnitt wirklich relevant:

#### Eine Timeline erstellen

Um diese zu erstellen, müssen die Offsets der Partitionen "System" und "Data" ermittelt werden.\
Mittels Sleuthkit beide extrahieren\
Mit mactime eine gruppierte und eine ungruppierte Liste erstellen\
als CSV importieren

Und.. ja. Das war's. 

Einlesen, was es mit den WAL-Dateien (Write Ahead Logs) auf sich hat, und wann man eher Sleuthkit / Autopsy nutzen sollte - Sleuthkit ignoriert WAL-Files, Autopsy fügt sie mit ihren Datenbanken zusammen.

