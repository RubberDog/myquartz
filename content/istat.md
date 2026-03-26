istat bietet die gleiche Möglichkeit zur Betrachtung von [[timestamps]] wie das Commandline-Tool [[stat]], jedoch wird hier eine inode statt eines Dateinamens angegeben.
Dies wird benutzt, um auf Dateien in mittels [[xmount]] gemounteten Images zuzugreifen.
Durch die Benutzung von [[fls]] mit dem Beispielhaften Befehl 
`fls -pr /dev/loop0p2 | grep -i SAM$` 
kann die jeweilige inode ausgegeben werden:

![[Pasted image 20260326110250.png]]

(*Erläuterung zum oben ausgeführten Befehl unter [[fls]]*)

Die Anzeige von 
`istat /dev/loop0p2 59953` zeigt dann die [[timestamps]] und weitere Informationen;

![[Pasted image 20260326110627.png]]