
------------------
Begriffe / Definitionen

Hacker - konkrete oder abstrakte Person oder Gruppe\
Opfer - (target); Organisation oder Person, als "target" auch konkretes IT-System\
Angreifer - oft synonym "hacker"
- Eavesdropper: hört Kommunikations ab / sieht Kopien ein. Nicht oder kaum wahrnehmbar aktiv
- Janus-Angreifer (MitM) - klassisch: gibt beiden Kommunikationsbeteiligten gegenüber vor, der jeweils andere zu sein
Verteidiger - obvious. Opfer != Verteidiger\
Wert (Asset) - Elemente einer IT-Umgebung, die relevant für den Angreifer sind\
Bedrohung (Threat) - benennt einen möglichen Wert des Angreifers zum Asset\
Schutzziel - abstraktes Konzept gegen welche Art Schadenswirkung eine Absicherung erforderlich ist
- Vertraulichkeit (Confidentiality) - nur autorisierte Akteure dürften Daten einsehen
- Integrität (Integrity): nur autorisierte Akteure dürfen Daten schreiben
	-  Datenintegrität; Daten dürfen nur von autorisierten Akteuren geschrieben, geädert, gelöscht werden.
		- Maßnahmen: Schreibschutz-Kotrollen, Hashwert-Vergleich, digitale Signaturen
	- Herkunftsintegrität: Aktivitäten im System können zweifelsfrei autorisierten Akteuren zugeordnet werden. 
		- Maßnahmen: Passworteingaben, biometrische Verfahren, Durchsetzung Rechte-Konzept (Access Control)
	- Zutrittskontrolle: Nur autorisierte Akteure haben physischen Zutritt zu Räumen mit IT-Komponenten
		- Maßnahmen: Schlösser, Zäune, Wachpersonal
	- Zugangskontrolle: Nur autorisierte Akteure dürfen Aktionen auf IT-Systemen auslösen.
		- Maßnahmen: Benutzerkonten mit Login auf Betriebssystem- oder Websystem-Ebene
	- Zugriffskontrolle: Nur autorisierte Akteure dürfen auf konkrete Daten eines konkreten Systems zugreifen.
		- Maßnahmen: Zugriffsrechte auf Dateisystem- oder Datenbankebene, Protokollierung und Logging
- Verfügbarkeit (Availability): Systeme sind für sämtliche Akteure auf ihrer jeweiligen Ebene der Autorisierung jederzeit erreichbar
	  
MERKEN: CIA\
	Confidentiality
	Integrity - Beide Arten;
	- Integrität, Herkunft (Login sagt: Wer war's) und 
	- Daten (Hash: passt?) an sich, dann Unterteilung Tür -> System -> Daten)
	Availability
		

Weitere Schutzziele:
- Authentizität (authenticity): Ist der Akteur tatsächlich die Person, die sie vorgibt zu sein (biometrie, Kenntnis)
- Autorisation (authorization): Ist der zuvor authentifizierte Akteur für eine spezifische Aktion berechtigt?
- Zurechenbarkeit (accountability): Kann jede Aktion einem Akteur eindeutig zugewiesen werden
- Transparenz (transparency): Daten und sie verarbeitende Prozesse den betroffenen Personen jederzeit, vollumfänglich und verständlich zugänglich machen
- Intervenierbarkeit (intervenability): Betroffenen Personen die möglichkeit geben, die Datenverarbeitung zu beenden / einzuschränken, Daten zu löschen / berichtigen
- Nichtverkettbarkeit (unlinkability): Personenbezogene / personenbeziehbare Daten dürfen nicht in anderem Kontext als dem, für den sie erhoben wurden genutzt werden. Daten aus verschiedenen Quellen dürfen nicht verglichen / verkettet werden.
- Betriebssicherheit (safety): Anforderungen an den Betrieb eines (IT-)Systems, um körperliche und geistige Unversehrtheit der an den Maschinen arbeitenden Personen zu gewährleisten.

MERKEN: TANZBÄR (geschrieben: TANZBIA)
- Transparenz
- Authentifizierung
- Nichtverkettbarkeit
- Zurechenbarkeit
- Betriebssicherheit
- Intervenierbarkeit
- Autorisation
			
Wichtig für die Reihenfolge:\
	Erst "Wer bist du", dann "Was darfst du"
	
			

Ziele eines PenTest:
	1. Möglichst viele Schwachstellen identifizieren
	2. Sämtliche gefundene Schwachstellen und Angriffswege der IT-Komponenten im Scope des PenTest dokumentieren
	3. Keine tatsächlichen Schäden für den Produktivbetrieb des IT-Systems im Rahmen des PenTest erzeugen

Dementsprechen NICHT Ziel:
	1. Schnellstmöglich Admin-Zugang zu den IT-Komponenten erlangen
	2. Tatsächliche Schäden auslösen

Ablauf PenTest:
	1. Beauftragung: Identifikation der Notwendigkeit
	2. Festlegung von Verantwortlichkeiten: In-House oder Extern
	3. Festlegung des Scope: Was darf / darf nicht angegriffen werden
	4. White- Grey- Blackbox
		1. Whitebox: Der Angreifer bekommt vorher alle relevanten Unterlagen zum Zielsystem, PenTest ist nur noch abprüfung dieser Systeme auf mögliche Schwachstellen
		2. Blackbox: Keine Infos außer Scope-Definition. Zeitaufwendiger, daher teurer. Aber: bessere Simulation eines realen Angriffs
		3. Greybox: Teilinformationen werden gegeben, Rest muss selbst identifiziert werden
	5. Festlegung des Zeitrahmens: Zeitrahmen und Zeitbudget
	6. Festlegung von Art und Modalitäten der Ergebnisdokumentation und -besprechung: Techniken des Angriffs i.d.R. irrelevant, gefundene Schwachstellen dagegen sehr wichtig
	7. Festlegung von Verantwortungen und Schadensersatzleistungen: Was passiert / Wer haftet bei Versehentlichen Schadensfällen während des PenTest

BSI-Leitfaden für Pentests enthält unter anderem die folgenden Anforderungen:
	- Test-Team aus mindestens zwei Personen wegen der 4-Augen-Prinzips
	- Prüfer / Prüfstellen sollten nie ohne schriftlichen Auftrag testen, daher sollte immer ein Vertrag zwischen Prüfern und zu testender Institution geschlossen werden
	- Sind Dienste zu Hostern ausgelagert, muss auch dieser in den Vertrag einbezogen werden
	- Der Vertrag sollte Rahmenbedingungen wie Prüfzeitraum, Prüfobjekt und Prüftiefe spezifizieren
	- Vereinbarungen zu Haftbarkeit und Verschwiegenheit sollten getroffen werden
	- Vertrag sollte beinhalten, dass gefundene Ergebnisse nur zum Zeitpunkt der Tests gültig sind und wegen eventueller Beschränkungen nicht gewährleistet ist, dass alle Fehler gefunden werden
	- Datenschutz muss zu jeder Zeit gewährleistet bleibt. Wenn Personenbezogene Daten betroffen sind, so muss der Datenschutzbeauftragte und ggf. auch die Personalvertretung vor den Tests einbezogen werden
	- Betroffene Personenkreise solltn vor dem Test benachrichtigt werden, um Unmut zu vermeiden
	- Bei den gewählten Zeiträumen sollte beachtet werden, keinen Wartungszeitraum zu nutzen

Cyber-Kill-Chain
1. Reconnaissance
2. Weaponization
3. Delivery
4. Exploitation
5. Installation
6. Command and Control
7. Actions on Objective

Simples Bild zum merken: Das (echte) trojanische Pferd:
- Reconnaissance: Der Herrscher liebt Anerkennung jeglicher Form
- Weaponization: Das Holzpferd wird gebaut (Zero-Day)
- Delivery: Es wird vor dem Tor abgestellt 
- Exploitation: Man nutzt die Schwachstelle des Herrschers aus, Pferd wird innerhalb der Mauer platziert 
- Installation: Nachts steigen die Soldaten aus 
- C&C: Besprechung der Angriffsziele 
- Actions: Ausführung, die relevantesten Punkte (z.b. das Tor und Wachen direkt daran) werden beseitigt, der Rest der Soldaten betritt die Stadt

Social Engineering:
- Spear Phishing
	- gezieltes Phishing
- Pretexting
	- Angreifer gibt sich als Vertrauenswürdige Person / Organisation aus, um Informationen zu erlangen

Automatisierte Schwachstellensuche\
	Nessus\
	OpenVAS\
	Qualys Web Application Scanner\
	Metasploit\
	NMAP

Active Directory, Outlook, Office
	HIER AUSGELASSEN


Threat Modelling
- Definition des Systems oder der Anwendung, das analysiert werden soll
- Identifizieren von Bedrohungen
- Bewertung der Risiken 
- Priorisierung von Maßnahmen zur Risikominderung

Drei Systeme für Thread-Modelling;
- STRIDE
- OWASP Threat Dragon
- MITRE ATTA&CK Framework

STRIDE:
- Spoofing (Täuschen), Angreifer versucht falsche Identität anzunehmen um Zugriff zu erlangen - auch gefälschte Anmeldeinformationen
- Tampering (Manipulation), Angreifer manipuliert / ändert Daten, z.B. durch Zugriff oder Modifikation der Übertragung
- Repudiation (Leugnung), Angreifer kann leugnen, z.B. weil es keine  oder manipulierte Logs gibt
- Information Disclosure (Offenlegung von Informationen), das ungewollte offenlegen sensibler Informationen, z.B. durch unsicher Datenübertragung / falsche Berechtigungen
- Denial of Service (Dienstverweigerung), (D)DoS
- Elevation of Privilege (Erhöhung von Rechten), Angreifer versucht eigene Berechtigungen im System zu erhöhen

OWASP Threat Dragon
- Software, mal anschauen - offenbar nicht weiter prüfungsrelevant

MITRE ATT&CK Framework
- Adversarial Tactics, Techniques, and Common Knowledge
	 - Aktualisierung und Pflege durch die Community

Keine weiteren Detail-Infos. Links auf S. 33 PDF

Training:
- CTF
- Cyber Ranges
- Security Awareness Trainings

Links auf S. 37

Weitere verwandte Konzepte
- Bug Bounty
- Auditierung und Zertifizierung
	- ISO 270001 (Information Security Management Systems)
	- ISO 9001 (QM-Systeme)
	- IT-Grunschutz nach BSI
	- Common Criteria for Information Technology Security Evaluation
- Software Testing
- RE (Reverse Engineering)
- Ethische Aspekte
	- Responsible Disclosure
	- Full Disclosure
- Rechtliche Aspekte

-------------------

Genannte Tools:
- Nessus
- OpenVAS
	- Ist ein Open-Source-Vulnerability-Scanner
- Qualys Web Application Scanner
	- Ist ein Cloudbasiertes Schwachstellen-Management-Tool
- Metasploit
- NMAP

(Links dazu auf Seite 28, PDF)
