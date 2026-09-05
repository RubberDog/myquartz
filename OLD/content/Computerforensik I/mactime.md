`mactime -b bodyfile > timeline.gruppiert` ist das Beispiel aus [[VL 24.03.2026]]

 `mactime` ist ein Tool, welches eine ASCII-Timeline aus Datei-Aktivitäten erstellt.\
`-b bodyfile` besagt, dass die Eingabe ein "body"-File ist und gibt den Pfad zur Datei an - hier relativ, da im gleichen Verzeichnis. Dieses bodyfile kann z.B. von [[fls]] erstellt werden.\
`> timeline.grupppiert` sagt, dass der Output in eine Datei namens "timeline.gruppiert" geschrieben werden soll.

In der [[VL 24.03.2026]] öffnet HPM das Ergebnis dann in einem grafischen Texteditor namens "pluma". Einfach nur, weil man da einfach scrollen kann.

Die Ausgabe von mactime ist sortiert, so dass Dateien die zeitgleich in irgendeiner Form geändert wurden, als Cluster dargestellt werden.\
In der vierten Spalte finden sich die Abkürzungen `MACB` aus den [[timestamps]] wieder, welche angeben, was zur Zeit in Spalte eins mit dieser Datei gemacht wurde.

Eine weitere, relevante Option um nicht nach dem Zeitpunkt suchen zu müssen, zu dem eine Datei eingruppiert ist:\
`mactime -d -b bodyfile > timeline.ungruppiert`\
Das macht aus der Timeline quasi eine .csv-Datei, die einzelnen Werte sind durch Kommata getrennt.\
Der relevante Vorteil jedoch; Die Dateien werden nicht mehr gruppiert nach Zeitpunkt angezeigt, sondern jede Datei hat einen eigenen Timestamp in der ersten Spalte.\
Durch `cat timeline.ungruppiert | grep "Dateiname"` kann ich also gezielt nach einer einzelnen Datei suchen und bekomme den passenden Zeitstempel direkt dazu.

Kurze Hinweise;\
Möchte man angeben, wie viele Einträge diese Timeline hat, so bietet sich der Befehl\
`cat timeline.gruppiert | wc -l` an, welcher den gesamten Inhalt der Datei wiedergibt, aber direkt in das Programm `wc` mit der Option `-l` übergibt, was die Anzahl der Zeilen zählt.\
Genauso relevant, mittels `tail -n 20 timeline.grupppiert` kann man sich die letzten 20 Zeilen ausgeben lassen.\
Dies ist hilfreich, um z.B. direkt sagen zu können dass ein Gerät seit 2018 nicht mehr benutzt wurde, somit es für eine Straftat in 2025 vermutlich nicht relevant ist.