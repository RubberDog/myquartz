
Grundsätzlicher Ablauf:

Image (.E01 (EWF, Expert Witness Format)) herunterladen.

Wegen des Speicherzugriffsfehlers, bedingt in der Nutzung von libewf / libewf2 sollten alle genutzten Images vor der Auswertung mit Sleuthkit-Tools mittels [[xmount]] wieder in das raw-Format überführt werden.\
Die entstandene raw-Datei (.dd) wird dann mittels [[mmls]] betrachtet und mit [[losetup]] auf ein Loop-Device gelegt um es von dort zu mounten.\
Randnotiz; Aktuelle Ubuntu nutzen wegen der Snap-Architektur schon auf einer frischen Installation viele Loop-Devices, HPMs Empfehlung ist daher, wie auch die aktuelle 4n6-VM, ein Debian zu nutzen.

[[stat]]
[[istat]]
[[fls]]
[[mactime]]
[[icat]]
[[regripper]]
[[vshadowinfo]]
[[vshadowmount]]
[[readpst]]
[[sccainfo]]
[[timestamps]]
[[Klausurtipps]]

VL 24.3. bis -1:20:17