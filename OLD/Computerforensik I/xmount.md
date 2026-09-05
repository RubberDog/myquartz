Mittels xmount kann ein Festplatten-Image zwischen verschiedenen Formaten hin- und herkonvertiert werden.

Der Aufruf hierfür lautet (von .E01 zu .dd):\
`sudo xmount --in ewf filename.E01 --cache /tmp/filename.ovl --out raw /ewf`

`sudo` muss sein, wenn man nicht eh als root unterwegs ist. Auf HPMs Website leider nicht so richtig ersichtlich.

`--in` erwartet das Eingabeformat, hier `ewf`, sowie die Datei.\
Unterstützte Formate sind:
- raw (dd)
- ewf (Expert Witness Compression Format)
- aff (Advanced Forensic Format v3)
- vdi (VirtualBox Virtual Disk Image) und 
- qcow (QEMU Copy on Write).

Wichtig: gibt es mehrere Dateien ( dell3.E01, dell3.E02, ...) so können diese NICHT einzeln via xmount konvertiert werden, das gibt nen Fehler.\
Stattdessen müssen entweder alle Dateien hintereinander im Aufruf angegeben werden;\
`sudo xmount --in ewf dell3.E01 dell3.E02 --cache /tmp/dell.ovl --out raw /ewf`
oder mittels Sternchen alle erfasst werden;\
`sudo xmount --in ewf dell3.E0* --cache /tmp/dell.ovl --out raw /ewf`\
Hier darauf achten, dass nur .E01 - .E09 erfasst werden. Gibt es mehr (.E10 oder mehr) muss das Sternchen entsprechend direkt hinter dem .E sitzen.

`--cache` ist da, um einen write-Cache zu geben - dadurch kann das entstandene Image z.B. gebootet werden, da hier notwendige Schreiboperationen abgelegt werden, um das tatsächliche Image im Originalzustand zu belassen

`--out` erwartet wieder ein Format, hier `raw`, sowie ein leeres Verzeichnis.\
Unterstützte Formate sind:
- raw (dd)
- dmg (Apple's Disk Image format)
- vdi (VirtualBox Virtual Disk Image)
- vhd (Microsoft Virtual Hard Disk Image) und 
- vmdk (VMWare Virtual Machine Disk)

Wichtig: In der 4n6-VM existiert `ewf` noch nicht - vorher anlegen! (`sudo mkdir /ewf` oder ein beliebiges anderes Verzeichnis)

Weiter geht's dann in [[losetup]]
