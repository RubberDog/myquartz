# Entity-Relationship-Modell

Relationen werden in den Inhalten von Woche3 HIER EIN LINK erklärt.

Um eine komplette Datenbank zu designen, müssen Relationen erstellt werden.\
Zur guten Handhabung und verminderung von Redundanzen wird Normalisierung HIER EIN LINK genutzt.\
Da der Entwurf einer solchen Datenbank, welche als einzige Redundanz Primär- und Fremdschlüssel besitzen sollte, nicht trivial ist nutzt man das vielfach bewährte ER-Modell.

### Entitäten

| Begriff | Bedeutung | Beispiel(e) |
| --- | --- | --- |
| Entität | Ein eindeutig unterscheidbares Objekt bzw. ein unterscheidbares Element | Person, Werkzeug, Produkt, Rechnung |
| Eigenschaft | Ein Teil einer Entität, welche diese Entität beschreibt | Name, Vorname, PLZ, Ort, Preis |
| Beziehung | Eine Entität, die zwei oder mehr Entitäten miteinander verknüpft | Die Entitäten Verkäufer und Produkt stehen in einer Beziehung: Verkäufer verkaufen Produkte | 
| Subtyp | Eine Entität, die Teil einer anderen, umfassenderen Entität ist | Die Entität Verkäufer ist ein Subtyp zu Mitarbeiter |
| Supertyp | Eine Entität, die Subtypen besitzt | Die Entität Mitarbeiter ist ein Supertyp von Verkäufer |
| Schwache Entität | Eintität, die von einer anderen Eintität vollständig abhängig ist | Die Entität Arbeitszeit ist schwach gegenüber der Entität Mitarbeiter |

Alle eindeutig identifierzierbaren Objekte werden als Entitäten bezeichnet, egal ob es Personen, Rechnungen auf Papier oder nur elektronische Daten sind.\
Objekte haben Eigenschaften; 
- Personen haben einen Namen
- Produkte haben einen Preis und ggf. ein Mindesthaltbarkeitsdatum
- Rechnungen haben ein Datum und eine Anschrift

Objekte haben Beziehungen zueinander;\
Eine Person ist ein Mitarbeiter, z.B. ein Verkäufer. Dieser verkauft Produkte und erstellt dafür Rechnungen.

Verschiedene Arten von Mitarbeitern sind Subtypen der Entität Mitarbeiter; Verkäufer, Informatiker, Schreibkräfte.\
Somit ist Mitarbeiter auch ein Supertyp der verschiedenen Teilgruppen.\
Wenn eine Entität Arbeitszeit pro Mitarbeiter erfasst wird, so ist diese schwach gegenüber der Entität Mitarbeiter - ohne Mitarbeiter kann die Arbeitszeit nicht existieren.

Das folgende Bild zeigt den Zusammenhang zwischen einer Entität und Eigenschaften:\
Eine Person hat
- ein Gehalt
- eine Adresse
    diese besteht aus
    - Strassenname
    - Hausnummer
    - PLZ
    - Ort
- einen Namen
    bestehend aus
    - Vorname
    - Nachname

![[Pasted image 20260411154030.png]]

In diesem Beispiel ist das ganze noch einfach zu überblicken, in großen Datenbanken kann schnell die Übersicht verloren gehen, weswegen strukturiert vorgegangen werden sollte.\
Da jedoch bei dieser Darstellung auch schnell der Platz ausgeht, gibt es eine an die UML angelehnte Darstellungsform, in der die Eigenschaften direkt in die Entität aufgenommen werden:\

![[Pasted image 20260411154234.png]]

Ein Beispiel für Beziehungen lässt sich einfach mit den Entitäten "Abteilung" und "Person" darstellen - Eigenschaften der Entitäten werden aus Übersichtsgründen nicht aufgeführt:\

![[Pasted image 20260411155126.png]] bzw. in Kurzform: ![[Pasted image 20260411155144.png]]

Das ist auch schon das Prinzip des ER-Modells. Entitäten und ihre Beziehungen zueinander, inklusive einer Anzahl.\
Zur Lesart: Hier handelt es sich um eine "m zu 1" Beziehung - immer vom kleineren zum geößeren hin.

#### Subtypen

Subtypen beziehen sich immer auf Supertypen.\
Sie existieren nicht nur zur besseren Unterscheidung, sondern haben meist auch spezielle Eigenschaften, die kein anderer Subtyp benötigt.\
Im Beispiel des Subtyp Verkäufers des Supertyp Mitarbeiter könnte es hier z.B. die Eigenschaft "Verkaufszahlen" geben.\
Wichtig: Eigenschaften des Supertyps werden immer übernommen. Also hat auch ein Verkäufer, wie jeder Mitarbeiter, z.B. einen Namen und eine Adresse.

Mehr zu Subtypen gibt es HIER EIN LINK

#### starke und schwache Entitäten

Schwache Entitäten wurden bereits erwähnt, sie sind voll abhängig von anderen Entitäten. Starke Entitäten hingegen können auch allein existieren.\
Ein Beispiel hierzu:\
Eine Entität Produkt besteht aus vielen Entitäten Einzelteil. Diese Einzelteile können aber auch ohne das Produkt existieren und für andere Produkte verwendet werden, sind also eine starke Entität.\
Eine Entität Fehlerliste, die sich auf das Produkt bezieht und festgestellte Fehler sammelt. Ohne ein Produkt kann es aber keine Fehlerliste geben bzw. wird sie wertlos, somit handelt es sich um eine schwache Entität.

![[Pasted image 20260411155340.png]]

Wollen wir eine Entität in SQL anlegen, so wird der `CREATE TABLE` Befehl genutzt - hier ein Beispiel für die Entität Person:\
```
CREATE TABLE Person
( Persnr     INTEGER,
  Vorname    CHARACTER(20),
  Nachname   CHARACTER(20),
  ...
  PRIMARY KEY (Persnr)
);
```


### Beziehungen

Hinweis: Im Script sagt ARD, dass es verschiedene Notationsformen gibt. Auch auf Wikipedia findet man verschiedene.\
Die "einfache" Notationsform würde ich - ebenso wie sie - empfehlen, es sei denn man ist schon eine andere gewohnt.\
Ein Beispiel zur einfachen Notation findet sich hier HIER BLOCK-TEXT-LINK ZU ZEILE 56

Beziehungen zwischen einzelnen Entitäten werden durch Fremdschlüssel (auch bekannt als Foreign-Key) hergestellt.

Es gibt in Datenbanken Primär- und Fremdschlüssel (primary key und foreign key). Beide sind eigentlich nur eindeutige Bezeichner eines Datensatzes, üblicherweise eine Fortlaufende Zahl die pro Zeile in einem Table vergeben wird, um Einträge zu identifizieren.\
Der einzige Unterschied zwischen Primär- und Fremdschlüssel: Ein Primärschlüssel befindet sich immer im **eigenen** Table, ein Fremdschlüssel ist ein Primärschlüssel eines **anderen** Table.

Diese Fremdschlüssel sollen hier identifiziert und erzeugt werden.\
Zuerst zeichnet man im ER-Modell sämtliche Entitäten ein. Danach überlegt man, in welcher Beziehung die Entitäten zueinander stehen. Am Ende sollte jede Entität mindestens eine Beziehung zu einer anderen Entität aufweisen.\
Das Ergebnis kann dann relativ einfach in eine relationale Datenbank übertragen werden.

Es gibt drei Grundlegende Kategorien von Beziehungen:
- 1 zu 1 Beziehungen
- m zu 1 (viele zu 1) Beziehungen
- m zu n (viele zu viele) Beziehungen

Eine 1 zu 1 Beziehung zwischen zwei Entitäten A und B ist gegeben, wenn jeder Eintrag in A eine Verbindung zu einem Eintrag in B - und umgekehrt - aufweist.\
Bei m zu 1 Beziehungen haben können mehrere Einträge in A auf einen einzigen Eintrag in B verweisen.\
Und bei m zu n Beziehungen funktioniert dies auch umgekehrt, so dass es beliebig viele mehrfache Zusammenhänge zwischen A und B geben kann.

Es gibt aber auch noch Sonderfälle. Um beim Beispiel einer Firma mit Personen und Abteilungen zu bleiben ist es auch möglich, dass jemand keiner Abteilung zugeordnet ist. Das Buch nennt hier z.B. Prokuristen oder Stabsstellen.\
Ein solcher Fall wäre eine "m zu 0 oder 1"-Beziehung, vereinfacht als "m zu c"-Beziehung. Wichtig hierbei ist, dass "c" nur die Werte 0 oder 1 annehmen kann.\
Ebenso kann auch eine Abteilung temporär 0 Personen haben, die ihr zugeordnet sind.

Es gibt daher folgende, wesentlichen **Beziehungswerte**:
- c (0..1)
- 1
- m

Geht man die möglichen Kombinationen dieser Werte durch gäbe es insgesamt 9 Fälle.
`1 zu 1` Beziehungen gibt es in der Praxis eigentlich nicht, `c zu 1` und `1 zu c` sind identisch, ebenso `c zu m` und `m zu c`, sowie `1 zu m` und `m zu 1`.

Die übrigen 5 Fälle sind:

1 zu c:\
Diese Fälle sind selten und meist anzutreffen, wenn Zusatzeigenschaften von Entitäten in Subtypen ausgelagert werden, um beispielsweise viele "0"-Einträge in einer Datenbank zu vermeiden, weil die Eigenschaft kaum vorkommt.\
Als Beispiel wieder Verkäufer und Mitarbeiter: Der Supertyp enthält alle Angaben zu den Mitarbeitern, der Subtyp zusätzliche Angaben zu Verkäufern - wie die zuvor genannte Eigenschaft "Verkaufszahlen".\
Somit wäre jeder Eintrag in der Entität "Verkäufer" auch ein mal in der Entität "Mitarbeiter" vorhanden, und zu jedem Mitarbeiter gibt es einen oder keinen Eintrag in der Entität Verkäufer.

c zu c:\
Ebenfalls ziemlich selten, die meisten eins-Beziehungen beruhen auf Sub- zu Supertyp und sind über 1 zu c behandelt, c zu c sind ein Spezialfall von m zu c und werden dort behandelt.

m zu 1:\
Hier verweisen kein, ein oder mehrere Einträge einer Entität auf genau einen Eintrag in einer anderen. Umgekehrt verweist jeder Eintrag in B auf genau einen Eintrag in A.\
Am Beispiel von Abteilung und Person: Zu jeder Abteilung gehört kein, einer oder mehrere Personen. Jedoch ist jede Person genau einer Abteilung zugeordnet - Sonderfälle wie zuvor erwähnt ausgenommen.\
Diese Form der Beziehung kommt häufig vor, beispielsweise in Hierarchien.

m zu c:\
Erneut das Beispiel der Abteilung und Person, wobei hier der Sonderfall abgebildet werden kann, dass eine Person auch (temporär) keiner Abteilung zugeordnet ist.

m zu n:\
Beide Variablen sagen aus, dass es temporär keine, eine oder viele Verknüpfungen zwischen den Entitäten geben kann.\
Beispiel hierzu wären die Entitäten Verkäufer und Produkt.\
Jeder Verkäufer kann viele verschiedene Produkte zum Verkauf anbieten, und jedes Produkt kann von vielen Verkäufern gleichzeitig angeboten werden.\
Ebenso kann ein neues Produkt existieren, ohne dass es verkauft wird, oder aber ein neuer Verkäufer hat noch keine Produkte, die er verkauft.

Im Buch (Erwin Schicker, Datenbanken und SQL, 5te Auflage von 2017) findet sich noch eine Tabelle mit mehreren Beispielen und Erklärungen auf Seite 85 (Buchnummerierung) bzw. Seite 97 (PDF-Nummerierung).


### Beziehungsrelationen

Nachdem im ersten Schritt alle Entitäten in Relationen überführt und im zweiten Schritt die Beziehungen zwischen den Entitäten betrachtet wurden, sollen jetzt diese einzelnen Beziehungen zwischen zwei Relationen betrachtet und geeignete Fremdschlüssel festgelegt werden.\
Die zuvor genannten fünf Beziehungen sollen jetzt unter diesem Gesichtspunkt erneut betrachtet werden.

#### `m zu n`-Beziehungen:\
Hier haben wir gleich den nervigsten Fall. Pro Zelle einer Datenbank darf nur ein einziger Wert stehen. Bei einer `m zu n`-Beziehung müsste ich aber `n` Werte hinterlegen, um diese Beziehung darzustellen.\
Daher müssen diese in eine eigene Relation (Tabelle) mittels Fremdschlüssel zusammengefübhrt werden.\
Hier ein Beispiel;

Table Student\
| id | name |
| --- | --- |
| 1 | Anna |
| 2 | Karl |

Table Kurs\
| id | Titel |
| --- | --- |
| 101 | Computerforensik |
| 102 | Datenbanken 1 |
| 103 | Cybercrime 2 |

Beide Studierenden belegen alle drei Kurse, und jeder Kurs hat somit zwei Studierende.\
Da ich nur einen Wert pro Zelle eintragen darf, wäre das hier nicht möglich. Daher erstellt man einen dritten Table, der z.B. so aussieht:\

Table Student_Kurs\
| student_id | kurs_id |
| --- | --- |
| 1 | 101 | 
| 1 | 102 |
| 1 | 103 |
| 2 | 101 |
| 2 | 102 |
| 2 | 103 |

----------------------
Nun folgt ein Ausflug in die wundervolle Welt der nested Queries bzw. JOINs..

Über diese Zwischentabelle kann ich nun mittels verschachtelter Abfrage HIER EIN LINK (hässlich aber machbar) oder mittels JOIN-Statement HIER EIN LINK einfach schauen, wer welchen Kurs belegt hat oder welcher Kurs welche Teilnehmer hat;\
```
SELECT titel
FROM Kurs
WHERE id IN (
    SELECT kurs_id
    FROM Student_Kurs
    WHERE Student_id = (
        SELECT id
        FROM Student
        WHERE name = 'Anna'
    )
);
```
Wichtig hierbei; das "IN" in der dritten Zeile. Ohne das würde die Abfrage nach dem ersten Ergebnis stoppen.\
Kurze Erklärung was hier passiert:\
Wir lassen uns die Titel aus dem Table Kurs ausgeben. Prinzipiell aber nicht alle, sondern nur für die, in denen die folgende Bedingung zutrifft:\
Die Kurs-ID aus dem Table Student_Kurs, für die Student-ID welche ich hierher bekomme:\
Die id aus dem Table Student mit dem zugehörigen Namen 'Anna'.\

Tipp bei nested querries; von hinten lesen ist einfacher, da man dann schon "einsetzen" kann:\
Ich ziehe die id aus dem Table "Student" mit dem Namen 'Anna'. Das Ergebnis ist eindeutig, nämlich '1'.\
Als nächste ziehe ich die kurs_id(s) aus dem Table Student_Kurs, wo die Student_id 1 ist.\
Durch das "IN" davor werden alle Ergebnisse dieser Sub-Abfrage behandelt, die da lauten: 101, 102, 103.\
Und jetzt werden die titel aus dem Table "kurs" gezogen mit den ids 101, 102, 103.

In hübscher mit JOIN:\
```
SELECT k.titel
FROM Student s
JOIN Student_Kurs sk ON s.id = sk.student_id
JOIN Kurs k ON sk.kurs_id = k.id
WHERE s.name = 'Anna';
```
Als kurze Erklärung:\
k.titel verweist auf die vierte Zeile, in der unser Table "Kurs" als alias einfach "k" bekommt. Wichtig, da wir aus dem Programmieren ja die Scopes (Lebensdauer von Variablen) kennen; Der alias "k" existiert ausschließlich in diesem einen query!\
Einmal alles aufgedröselt;

`SELECT k.titel` kommt erst ganz am Schluss. Wir wollen die Titel aus dem Table "Kurs" erhalten, deren Liste wir durch den Rest des Query abfragen.\
`FROM Student s` - der Table Student bekommt den alias `s`\
`JOIN Student_Kurs sk ON s.id = sk.student_id` - der Table "Student_Kurs" bekommt den alias "sk" und wird mit der Spalte "id" aus dem Table s (-> alias Student) kombiniert.\
Um sich das ganze vorzustellen: Es wird ein neuer, temporärer Table erzeugt.

ACHTUNG - In der Praxis "wissen" DBs durch Indexierung welche IDs, besonders wenn diese Fremdschlüssel sind, existieren. Daher kann direkt passend zugegriffen werden.\
Der ganze folgende Teil dient nur dem besseren Verständnis!

In diesem werden die Daten aus "s.id" mit allen Einträgen in "sk" kombiniert. Jetzt schaut SQL nach, wo "s.id" und "sk.student_id" identisch sind. Wo das nicht der Fall ist, werden die Zeilen verworfen. Wichtig: Dieser temporäre Table bleibt jetzt noch bestehen und wird weiter bearbeitet.\
Auch wichtig - einfach mal erwähnt, weil's mein Denkfehler war: in diesem temporären Table sind ALLE Spalten der beiden zusammengeführten Tables vorhanden, deren Zeilen den Filter bestanden haben.\
Hier ein Beispiel, wie der temporäre Table hier vor dem Filtern mit "ON s.id = sk.student_id" aussieht:\
| s.id | s.name | skstudent_id | sk.kurs_id |
| --- | --- | --- | --- |
| 1 | Anna | 1 | 101 |
| 1 | Anna | 1 | 102 |
| 1 | Anna | 1 | 103 |
| 1 | Anna | 2 | 101 |
| 1 | Anna | 2 | 102 |
| 1 | Anna | 2 | 103 |
| 2 | Karl | 1 | 101 |
| 2 | Karl | 1 | 102 |
| 2 | Karl | 1 | 103 |
| 2 | Karl | 2 | 101 |
| 2 | Karl | 2 | 102 |
| 2 | Karl | 2 | 103 |

Dann kommt der genannte Filter, es wird also überprüft, wo "s.id = sk.student_id". Nicht-übereinstimmende Zeilen werden verworfen.

`JOIN Kurs k ON sk.kurs_id = k.id` - der Table "Kurs" bekommt den alias "k" und wird unserem temporären Table hinzugefügt. Wieder in allen möglichen Kombinationen. Es wird alles verworfen, wo die Bedingung "sk.kurs_id = k.id" nicht zutrifft.

`WHERE s.name = 'Anna';` - wir haben bis hierhin noch Einträge von Anna und Karl - Karl ist uns egal, daher wird gefiltert, wo "s.name = 'Anna'" ist, der Rest wird verworfen.

Und jetzt wird das `SELECT k.titel` vom Anfang auf unseren temporären Table ausgeführt. Dieser hat nur noch Einträge, die zu "Anna" gehören. Hieraus wollen wir jetzt allerdings nur die Titel der Kurse.\
Die Ausgabe, die wir durch den SQL-Query erhalten lautet also:\
Computerforensik 1\
Datenbanken 1\
Cybercrime 2

Ende des Ausfluges in die wundervolle Welt der JOINs.

------------

Die zur Verknüpfung der Datensätze genutzten Fremdschlüssel sind immer eindeutig und bilden somit einen Schlüsselkandidaten.\
Bleiben wir beim Beispiel mit den Tables "Verkaeufer" und "Produkt", so würde der Table zur Verknüpfung dieser Daten beispielsweise die jeweiligen Primärschlüssel "VerkNr" und "ProdNr" nutzen.\
Erzeugen würde man diesen Table wie folgt:\
```
CREATE TABLE Verknuepfung
( VerkNr    CHARACTER(4)    REFERENCES Verkaeufer,
  ProdNr    CHARACTER(4)    REFERENCES Produkt,
  Umsatz    INTEGER,
  PRIMARY KEY (VerkNr, ProdNr)
);
```
Im hier angelegten Table werden Spalten für VerkNr und ProdNr aus den jeweiligen Tables, genannt hinter "REFERENCES", angelegt. In diese Spalten können nur Werte eingetragen werden, die in den referenzierten Tables und Spalten bereits existieren.\
Der Primary Key hier ist ein einzelner Wert, sondern eine Kombination. D.h., die Kombination aus VerkNr und ProdNr muss eindeutig sein und kann nicht mehrfach existieren. Es können jedoch 20 (oder mehr) Einträge mit der gleichen VerkNr vorhanden sein, solang sich die jeweils zugeordnete ProdNr unterscheidet.

Beziehungen werden im ER-Modell immer mit einer Raute bezeichnet.

#### `m zu 1`-Beziehungen
Auch `m zu 1`-Beziehungen lassen sich einfach in Beziehungsrelationen (einen neuen Table wie zuvor) überführen.\
Da es aber eine "zu 1"-Beziehung ist, ist es einfacher bereits beim erstellen der Tables, die verknüpft werden sollen, eine zusätzliche Spalte dafür zu erzeugen - hier am Beispiel "Person" und "Abteilung":
```
CREATE TABLE Person
( PersNr        INTEGER,
  Name          CHARACTER(25),
  ...
  Abteilungsnr    INTEGER NOT NULL REFERENCES Abteilung,
  PRIMARY KEY (Persnr)
);
```
Dadurch wird im Table "Person" beim Anlegen einer Person auch direkt eine Abteilungsnummer als Fremdschlüssel eingetragen - heisst, sie muss existieren. Neu ist hier der Zusart "NOT NULL". Dieser besagt, dass eine Angabe gemacht werden muss. Würde man versuchen dieses Feld leer zu lassen, bricht das Anlegen mit einem Fehler ab.

#### `m zu c`-Beziehung
Ist im Prinzip genau wie die `m zu 1`-Beziehung, der m-Beziehung wird ein Fremdschlüssel hinzugefügt. Einziger Unterschied ist, dass im Beispiel-Table oben die Bedingung "NOT NULL" ausgelassen wird, da `c` eben auch `NULL` sein kann und darf - es also möglich ist, dass die Person (temporär) keiner Abteilung zugeordnet ist.

#### `1 zu c`-Beziehung
Beinahe identisch mit der `m zu c`-Beziehung. Jedoch wird der Fremdschlüssel in relationalen Datenbanken zwingend der `c`-Beziehung hinzugefügt. Am Beispiel "Abteilung" und "Mitarbeiter":\
Die Abteilung erhält eine ID, einen Primary Key. Auf der Mitarbeiterseite wird diese Abteilungsnummer als Fremdschlüssel hinzugefügt - der Mitarbeiter kann, muss aber keine Abteilung haben. Also darf der Wert dort NULL sein.\
Die Abteilung hingegen muss zwingend eine Nummer zur Identifikation haben.

#### `c zu c`-Beziehung
Ist ziemlich selten, kann behandelt werden wie `m zu c` - mit der besonderheit, dass der Fremdschlüssel als `UNIQUE` markiert wird. Das Beispiel aus dem Buch finde ich zur Erklärung nicht so gut, besser:\
Ein Mitarbeiter hat keinen oder einen Firmenwagen. Genauso kann ein existierender Firmenwagen einer, oder aktuell keiner Person zugewiesen sein.


### Fremdschlüsseleigenschaften

weiter geht's auf pdf 102
