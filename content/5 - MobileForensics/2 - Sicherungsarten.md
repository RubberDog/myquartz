### Sicherung

Logische Sicherung:\
Es werden nur jene Daten erfasst, die dem Benutzer zugänglich sind. Gelöschte Daten sind dort nicht enthalten, es sei denn, sie sind lediglich als "zu löschen" markiert, es wurde aber noch nicht ausgeführt.

FullFileSystem:\
Alle Dateien auf dem Gerät. Es ist das komplette FileSystem, welches auf dem Gerät vorhanden ist.\
Wichtige Info: Bei Flash-Speichern wird nicht der gesamte Speicher des Systems vom Filesystem umfasst, sondern nur der Teil, der auch genutzt wird. (Im Detail etwas komplexer, aber auch das hier wird vom Skript nicht so genau erklärt).\
Das Skript sagt auch, dass die Betriebssystempartition hier nicht enthalten sei, sondern nur in einer physischen Sicherung - mag mal so gewesen sein, aktuell ist diese Aussage absolut falsch.

Physikalisch:\
Eine physikalische Sicherung ist nur bei alten Geräten möglich, die keine FileBasedEncryption (FBE) nutzen. Dabei können meist auch schon lange gelöschte Dateien wiederhergestellt werden, sofern sie noch nicht überschrieben wurden.