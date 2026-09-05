
## Begriffe

| Begriff | Bedeutung                  |
| ------- | -------------------------- |
| SQL     | Structured Query Language  |
| DBMS    | Database Management System |
| DDL     | Data Description Language  |
| DML     | Data Manipulation Language |
## Wichtige Anforderungen:

(Ab Seite 6 im Buch von Erwin Schicker)

Sammlung logisch verbundener Daten

Speicherung der Daten mit möglichst wenig Redundanz

Abfragemöglichkeit und Änderbarkeit von Daten

Logische Unabhängigkeit der Daten von der physischen Struktur HIER EIN LINK

Zugriffsschutz HIER EIN LINK

Integrität HIER EIN LINK

Mehrfachzugriff HIER EIN LINK

Zuverlässigkeit HIER EIN LINK

Ausfallsicherheit HIER EIN LINK

Kontrolle HIER EIN LINK


### DML

| Befehl | Wirkung                |
| ------ | ---------------------- |
| SELECT | zum Abfragen von Daten |
| UPDATE | zum Ändern von Daten   |
| DELETE | zum Löschen von Daten  |
| INSERT | zum Einfügen von Daten |
  
### DDL

| Befehl       | Wirkung                          |
| ------------ | -------------------------------- |
| CREATE TABLE | zum Erzeugen einer Tabelle       |
| DROP TABLE   | zum Löschen einer Tabelle        |
| CREATE VIEW  | zum Erzeugen einer Sicht         |
| GRANT        | zum Gewähren von Zugriffsrechten |
Mehr in Kapitel 5 HIER LINK (ODER BACKLINK)


## Datenbankmodelle

### relationale Datenbanken

Eine relationale DB besteht ausschließlich aus Tabellen, auch Relationen genannt.\
Ein Zugriff erfolgt immer über diese Tabellen.\
Hinzufügen, Löschen und Ändern der Datenbanken sowie die Zugriffe darauf sind sehr einfach umzusetzen, daher die Beliebtheit und weite Verbreitung.\
Die Zusammenhänge zwischen den Tabellen werden über Beziehungen hergestellt, welche in den Tabellen mit abgespeichert werden.\
Nachteil der relationalen Datenbanken sind, dass Zugriffe häufig das Lesen und Zusammenfügen von Informationen aus vielen Tabellen benötigen, was die Laufzeit verlängert und zu viel I/O führt, sowie dass manche Daten redundant gespeichert werden müssen, um sie in Tabellenform erfassen zu können.

Beispiele:
- Oracle
- DB2 von IBM
- SQL Server von MicroSoft
oder als Open-Source;
- MySQL
- PostgreSQL

### objektorientierte Datenbanken

Eine objektorientierte DB besteht ausschließlich aus Objekten, z.B. einer Person, einer Abteilung einer Firma, ein realer (Buch) oder abstrakter (Adresse) Gegenstand.\
Da viele Objekte auch in einer Tabellenform gespeichert werden können, werden objektorientierte Datenbanken häufig als Erweiterung relationaler DBs gesehen, was jedoch bestenfalls teilweise zutrifft.\
Ansätze wie Klassen, Datenkapselung und Vererbung kennt man z.B. aus der objektorientierten Programmierung.\
In der Praxis hat sich eine Mischform von objektorientierten und relationalen DBs durchgesetzt, die objektrelationalen DBs.\
Der Aufbau dieser ist komplexer, da mit komplexen Objekten statt einfacher Tabellen gearbeitet wird, was zu höherem Entwurfs- und Programmieraufwand führt. Auch die Verwaltung ist sehr aufwändig.\
Ein Vorteil ist jedoch, dass der Aufbau direkt der Realität entsprechen kann, und komplexe Objekte müssen nicht auf einfache Tabellen-Strukturen abgebildet werden.

Beispiele:
- Oracle
- DB2 von IBM
- PostgreSQL

### hierarchische und netzwerkartige Datenbanken

Hierarchischen Datenbanken wurden ab etwa 1960 eingesetzt, ihr logischer Aufbau entspricht einer Baumstruktur.\
Der Zugriff erfolgt immer über den Wurzelknoten hin zum gewünschten Knoten. Hierdurch wird eine sehr geringe Redundanz mit kurzen Zugriffszeiten erzielt, als Nachteil stellt sich jedoch die Inflexibilität bei Änderungen dar.\
Daher wurde dieses Modell durch die netzwerkartige Datenbank ergänzt.\
Der logische Aufbau besteht hier aus Daten, die über ein beliebig aufgebautes Netz verbunden sind. Dadurch wird die Flexibilität erhöht, jedoch steigt die Komplexität der Aufbaus enorm.\
Beide Modelle sind heute aufgrund der komplexen Zugriffe und Strukturänderungen quasi nicht mehr vorhanden.

Beispiele:
- IMS von IBM
- IDMS von Computer Associates
- UDS von Fujitsu

### Moderne Entwicklungen

Relationale Datenbanken sind auf Sicherheit bedacht, wobei der Transaktionsmechanismus besonders wichtig ist; jede Änderung innerhalb der Datenbanken wird sofort übernommen und ist sichtbar, was bei besonders großen Systemen enorme Rechenleistung erfordert - als Beispiele sind Facebook, Google, Amazon genannt.\
Für Internetabfragen ist meist jedoch nich relevant ob eine Information Sekundenaktuell ist, oder bereits 10 Minuten alt.\
Wird auf eine Sekundenaktualität verzichtet, so kann eine Aktualisierung auf verteilte Systeme performant erfolgen.\
Dies kann jedoch auch dazu führen, dass eine Abfrage an den nächstverfügbaren Server gestellt wird, der möglicherweise noch nicht den aktuellsten Stand erfasst hat.

Diese Systeme werden als NoSQL bezeichnet, welche grob in drei Modelle unterteilt werden können;

- Key/Value und dokumentenbasierte Modelle
- Spaltenorientierte Modelle
- Graphenorientierte Modelle

#### Key/Value und dokumentenbasierte Modelle

Diese Modelle sind Schemafrei, was bedeutet, dass der Aufbau der Datensätze nicht bereits beim Anlegen der Datenbank vorgegeben wird, sondern erst direkt vor der Eingabe eines Datensatzes definiert werden muss, so dass auch beliebige Dokumente oder binär kodierte Objekte abgelegt werden können.

Beispiele:
- DBM (Database Manager) von Ken Thompson (dokumentenbasiert)
- Lotus Notes von IBM (dokumentenbasiert)
- Berkly-DB (Key/Value)
- CouchDB (dokumentenbasiert)
- MongoDB (dokumentenbasiert)

#### Spaltenorientierte Modelle

Sie speichern Daten Spaltenweise statt Zeilenweise wie in relationalen DBs ab.\
Werden immer nur spezifische Eigenschaften gesucht, kann der spaltenorientierte Ansatz gegenüber dem zeilenorientierten zu Leistungssteigerungen führen.

Beispiele:
- BigTable von Google
- SimpleDB von Amazon
- HBase (Open Source)
- Cassandra (Open Source)

#### Graphenorientierte Modelle

Sie basieren auf der [Graphentheorie](https://de.wikipedia.org/wiki/Graphentheorie).\
Ihren größten Vorteil haben sie beim Speichern von Geodaten, das Traversieren einer Route ist deutlich performanter als mit herkömmlichen Datenbanken, besonders in Smartphones und Navigationsgeräten werden sie daher vermehrt genutzt.

Beispiele:
- Sones
- Neo4J


### Transaktionen

Es gibt drei Unterschiedliche Zugriffsarten:
- Abfragen (auch genannt Query)
- Mutation (Änderung)
- Transaktion

Abfragen HIER LINK und Mutationen HIER LINK sind inhaltlich selbsterklärend.\
Bei einer Transaktion handelt es sich um eine Operation, um die Konsistenz zu erhalten.\
Als Beispiel wird eine Überweisung zwischen zwei Konten einer Bank genannt;\
Neben den Kontoständen der Konten A und B wird üblicherweise auch ein Saldo gespeichert, also die Summe aller Kontostände.\
Wird nun von Konto A zu Konto B eine Summe x überwiesen, so wird diese zuerst von Konto A abgezogen, in einer zweiten Operation zu Konto B hinzugefügt.\
Zwischen diesen beiden Operationen existiert eine Inkonsistenz der Daten - da von Konto A eine Summe abgezogen, aber Konto B noch nicht gutgeschrieben wurde, ist das Saldo der Bank um Summe x höher, als die - zu diesem Zeitpunkt - tatsächliche Summe aller Kontostände.\
Während es sich also beim Abzug der Summe x von Konto A, als auch bei dem hinzufügen von Summe x zu Konto B jeweils um eine Mutation HIER LINK handelt, so ist die Gesamtheit der Operationen zur Wiederherstellung der Konsistenz - in diesem Fall also zwei Operationen - als Transaktion bezeichnet.

Konsistenz bezeichnet die Freiheit von Widersprüchen innerhalb einer Datenbank.\
Wichtig ist, dass eine Redundanz von Daten aufgrund ihres vielfachen Vorkommenns den Aufwand erhöht, um diese Daten konsistent zu halten.\
Zweitens heißt es im Buch, dass __alle__ Zugriffe in einer kommerziellen Datenbankanwendung zwingend Transaktionen sind.\
Das [[DBMS - Motivation#Begriffe|DBMS]] muss auch im Falle eines Rechnerabsturzes eine Konsistenz der Daten aufrecht erhalten. Daher sorgt es dafür, dass jede Transaktion [atomar](https://de.wikipedia.org/wiki/Atomare_Operation#Atomare_Datenbank-Operationen) abläuft

### Konsistenzmodell ACID

ACID ist eine Abkürzung für vier Eigenschaften, welche im Transaktionsbetrieb erwartet werden;
- **A**tomarity (Atomarität)
- **C**onsistency (Konsistenz)
- **I**solation
- **D**urability (Dauerhaftigkeit)

**Atomarity** bedeutet, dass jede Transaktion zusammenhängend und vollständig ausgeführt, oder gar nicht.\
Relationale Datenbanken haben dafür zwei wichtige Befehle;
- COMMIT;
	- beendet eine Transaktion
- ROLLBACK;
	- wird ausgeführt, wenn kein COMMIT; existiert - macht die Änderung Rückgängig


Kurze Erklärung die über das Buch hinaus geht, aber beim Verständnis hilft (kein einfaches "isso"):

Sendet ein Client Operationen an ein DBMS, so werden die Änderungen sofort ausgeführt, jedoch in einem [WAL-File](https://de.wikipedia.org/wiki/WAL-Prinzip) (**W**rite **A**head **L**og) gespeichert, welches je nach Konfiguration des Servers entweder periodisch fest in die Datenbank übernommen wird, oder nach erreichen einer festgelegten WAL-Datei-Größe.\
Stürzt der Server ab, während Änderungen ohne COMMIT;-Befehl im WAL-File vorhanden sind, so werden die Änderungen beim Neustart und dem damit verbundenen einlesen der WAL-File(s) verworfen.\
Stürzt der Client während der Übertragung von Operationen ab, so stellt der Server den Abbruch der Verbindung auf Netzwerk-Ebene (TCP/IP) fest. Schließt kein COMMIT; die übertragenen Änderungen ab, so werden sie sofort vom Server verworfen.

**Consistency** wird durch eben jene atomare Ausführung gewährleistet.

**Isolation** meint hier, dass im heute üblichen Mehrbenutzerbetrieb jede Transaktion so behandelt werden muss, als sei sie die einzige im System - Details dazu später HIER EIN LINK UND ANGEPASSTER NAME

**Durability** heißt tatsächlich nur ganz simpel, das einmal abgeschlossene Transaktionen bzw. abgespeicherte Daten nicht verloren gehen dürfen.