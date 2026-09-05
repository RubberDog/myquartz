
Achtung:\
Volume-Shadowkopien werden von Windows Vista bis Windows 10 automatisch angelegt.\
Seit Windows 11 muss der Benutzer explizit diese Art des Backup aktivieren, andernfalls existieren einfach keine Shadow-Kopien!

Volume-Shadowkopien werden vom System angelegt, sobald Windows ein Update startet.\
Ihre Größe ist identisch mit der Größe des Laufwerk `C`.

Zur Benutzung;\
`vshadowinfo /dev/loop0p2` - ziemlich einfach. Man gibt das Ziellaufwerk an, hier /dev/loop0p2 welches das Laufwerk `C:` beinhaltet. Das Ergebnis kann dann so aussehen;\

![[Pasted image 20260329155124.png]]

In diesem Fall existieren fünf Volume-Shadowkopien. Die Bytesize ist immer identisch, da es sich um eine bitgenaue Kopie des gesamten Laufwerks - auch leerer Speicherplatz - handelt.

Jetzt geht's auch schon weiter zu [[vshadowmount]].