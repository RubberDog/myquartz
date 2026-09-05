
Zu allererst; Achtet darauf, dass eure VM mit genügend CPU und RAM ausgestattet ist.
Das meiste klappt auch so, aber spätestens bei Plaso dauert's sonst sehr lange

Fangen wir an mit [[APL-Hinweise]]n

Weiterer Tipp;\
Arbeitet ihr dauerhaft als Benutzer `root` ist das aus IT-Sicherheitssicht zwar eine Vollkatastrophe, jedoch spart ihr euch nerviges Suchen wenn euer System mal behauptet ein Kommando nicht zu kennen, weil es nur für root zur Verfügung steht, oder einen Befehl nochmal aufzurufen, weil ihr das `sudo` am Anfang der Zeile vergessen habt.. passiert mir übrigens auch immer mal wieder.\
Für ein Grinsen nebenbei sei an dieser Stelle das Projekt [The Fuck](https://github.com/nvbn/thefuck) erwähnt.

Grundsätzlicher Ablauf:

Image (.E01 (EWF, Expert Witness Format)) herunterladen.

Wegen des Speicherzugriffsfehlers, bedingt in der Nutzung von libewf / libewf2 sollten alle genutzten Images vor der Auswertung mit Sleuthkit-Tools mittels [[xmount]] wieder in das raw-Format überführt werden - und auch, damit man (theoretisch) das Image booten kann, ohne etwas zu verändern.\
Die entstandene raw-Datei (.dd) wird dann mittels [[mmls]] betrachtet, um vorhandene Partitionen und Speicheroffsets abzulesen, und danach mit [[losetup]] auf ein Loop-Device gelegt um es von dort zu mounten.\
Randnotiz; Aktuelle Ubuntu nutzen wegen der Snap-Architektur schon auf einer frischen Installation viele Loop-Devices, HPMs Empfehlung ist daher, wie auch die aktuelle 4n6-VM, ein Debian zu nutzen.\

Das Image kann dann via [[fls]] nach einzelnen Dateien / Ordnern durchsucht werden.\
Weiß man nicht, was genau man eigentlich sucht, so kann man auch ganz normal durch das Dateisystem des gemounteten Images "wandern" und alles betrachten, mittels `cd` und `ls`.

Ein wichtiger Unterschied; gemountet habe ich nur Zugriff auf den logischen Teil des Dateisystems, also existente Dateien.\
Mit [[fls]] kann ich den gesamten gesicherten Bereich durchsuchen, also der physikalisch vorhandene Speicher.

Habe ich eine relevante Datei gefunden kann es als erster Schritt relevant sein, wann diese Datei zuletzt genutzt wurde. Im gemounteten Dateisystem nutze ich dafür [[stat]], möchte ich mir das direkt im Image ansehen, so kann ich [[istat]] unter Angabe des inode nutzen.\
Darüber finden sich alle relevanten [[timestamps]].

Möchte mir dann die Datei, oder als ersten Schritt unter Windows die Registry-Hives außerhalb zur genaueren Untersuchung sichern, mache ich das entweder "logisch" via `cp` über das Dateisystem, oder hole mir die Datei durch [[icat]] aus dem Image und schreibe sie z.B. in das `/tmp/`-Verzeichnis.

Für Registry-Hives empfiehlt sich der Einsatz von [[regripper]] mit seinen zahlreichen Plugins.\
Es ist jedoch keine Wunderwaffe - für die APL wird's wohl reichen, in der Realität bietet sich häufiger auch ein Blick via Registry-Editor o.ä. an, um ggf. auch Korrelationen bilden zu können, wie die GUID einer Festplatte mit den (hoffentlich) verfügbaren Infos zu Hersteller, Modell und Speicherkapazität in Verbindung zu bringen. 


---------
Work in Progress;

Timeline erstellen:  
- mit [[fls]] und [[mactime]], "normale Timeline"
- mit log2timeline, "Supertimeline" via Plaso - braucht auch bei kleineren Images ziemlich lange



- [[vshadowinfo]]
- [[vshadowmount]]
- [[fsstat]]
- [[sccainfo]]
- [[prefetch]]

ToDo

- [[readpst]]
- [[bulk_extractor]]
- [[mmls]]



VL 24.3. bis -1:20:17