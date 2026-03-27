`losetup` erstellt loop-Devices. Da wir hier unsere raw-Images mounten wollen, müssen diese entsprechend angelegt werden.

Dafür gibt es zwei möglichkeiten:\
Mittels [[mmls]] das Image und die darauf vorhandenen Partionen betrachten:\
`mmls /ewf/i9300.dd`\
hier am Beispiel eines Samsung Galaxy S3 (i9300) Smartphones;\
![[Pasted image 20260325104931.png]]

*(Weitere Erklärung zur Bedeutung der einzelnen Spalten in [[mmls]])*

Hier ist die Partition `USERDATA` relevant, die man via (Start-)Speichersektor direkt selektieren kann:\
`sudo losetup -o $((6586368*512)) /dev/loop1/ /ewf/i9300.dd`\
`sudo` ist wieder relevant, da nur root loop-Devices erstellen darf und normale User keinen Zugriff auf das Programm `losetup` haben.

Mittels `-o $((6586368*512))` wird das Offset - in Byte ! - angegeben. Hier in doppelten Klammern,  damit die Shell das Ergebnis des Sektors (6586368) mal die Sektorgröße, 512 Byte, errechnet.

`/dev/loop1` gibt das loop-Device an, welches genutzt werden soll, und `/ewf/i9300.dd` das Image, aus welchem der Speicherbereich stammen soll.

Einfacher geht das ganze, wenn man `losetup` sämtliche Partitionen des Image zuweisen lässt:
`sudo losetup --partscan --find --show /ewf/i9300.dd`

Schaut man sich dann einmal mittels `ll` (gleichbedeutend mit `ls -la`) den Inhalt von `/dev/loop0*` an, so finden sich hier alle Partitionen;

![[Pasted image 20260325105845.png]]

Weiter in [[fls]]
