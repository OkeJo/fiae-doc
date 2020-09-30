# SQL

**SQL oder SEQUEL** ist eine Datenbanksprache zum Kontrollieren und Erschaffen von Datenstrukturen in relationalen Datenbanken. 

Grundsätzlich sind folgende Operationen unterstützt: 

*CREATE, INSERT, ALTER, DELETE* 

also Erstellen, Einfügen, Verändern und Löschen.

***Fun Fact: SQL (Structured Query Language) wurde erst nach rechtlichen Problemen mit Hawker Siddley Aircraft Company von SEQUEL (Structured English Query Language) umbenannt.***

## SQL Kategorisierung

SQL-Befehle lassen sich in vier Kategorien unterteilen

### DATA QUERY LANGUAGE (DQL)

Befehle zur Abfrage und Aufbereitung der Informationen. 

Wird auch als Untergruppe der DML klassifiziert

### DATA MANIPULATION LANGUAGE (DML)

Befehle zur Datenmanipulation (Ändern, Einfügen, Löschen von Datensätzen) und lesendem Zugriff

### DATA DEFINITION LANGUAGE (DDL)

Befehle zur Definition des Datenbankschemas (Erzeugen, Ändern, Löschen von Datenbanktabellen, Definition von Primärschlüsseln und Fremdschlüsseln)

### DATA CONTROL LANGUAGE (DCL)

Befehle für die Rechteverwaltung

### TRANSACTION CONTROL LANGUAGE (TCL)

Befehle für die Transaktionskontrolle

[https://de.wikipedia.org/wiki/SQL#/media/Datei:SQL.png](https://de.wikipedia.org/wiki/SQL#/media/Datei:SQL.png)

Mit Abfragen (Queries) werden die in einer Datenbank gespeicherten Daten abgerufen, also dem Benutzer oder einer Anwendersoftware zur Verfügung gestellt.

Das Ergebnis einer Abfrage sieht wiederum aus wie eine Tabelle und kann oft auch wie eine Tabelle angezeigt, bearbeitet und weiterverwendet werden.

### Einfache Abfrage

```sql
SELECT *
FROM Student;
```

### Abfrage mit Spaltenauswahl

```sql
SELECT VorlNr, Titel
FROM Vorlesung;
```

### Abfrage mit eindeutigen Werten (DISTINCT)

```sql
SELECT DISTINCT MatrNr
FROM hört;
```

### Abfrage mit Umbenennung (AS)

```sql
SELECT MatrNr AS Matrikelnummer, Name
FROM Student;
```

### Abfrage mit Filter (WHERE)

```sql
SELECT VorlNr, Titel
FROM Vorlesung
WHERE Titel = 'ET';
```

### Abfrage mit Filter nach Inhalt (LIKE)

```sql
SELECT Name
FROM Student
WHERE Name LIKE 'F%';
```

### Abfrage mit Filter und Sortierung (ORDER BY)

```sql
SELECT Vorname, Name, StrasseNr, Plz, Ort
FROM Student
WHERE Plz = '20095'
ORDER BY Name;
```

### Abfrage mit verknüpften Tabellen (JOINS)

```sql
SELECT Vorlesung.VorlNr, Vorlesung.Titel, Professor.PersNr, Professor.Name
FROM Professor
    INNER JOIN Vorlesung 
			ON Professor.PersNr = Vorlesung.PersNr;
```

### Zusammenfassung eines SELECT

```sql
SELECT [DISTINCT] Auswahlliste [AS Spaltenalias]
FROM Quelle [ [AS] Tabellenalias], evtl. mit JOIN-Verknüpfungen
[WHERE Where-Klausel]
[GROUP BY ein oder mehrere Group-by-Attribute]
[HAVING Having-Klausel]
[ORDER BY ein oder mehrere Sortierungsattribute mit [ASC|DESC]];
```

Erläuterung:

- DISTINCT gibt an, dass aus der Ergebnisrelation gleiche [Ergebnistupel](https://de.wikipedia.org/wiki/Tupel_(Informatik)) entfernt werden sollen. Es wird also jeder Datensatz nur einmal ausgegeben, auch wenn er mehrfach in der Tabelle vorkommt. Sonst liefert SQL eine Multimenge zurück.
- Auswahlliste bestimmt, welche Spalten der  auszugeben sind (* für alle) und ob [Aggregatfunktionen](https://de.wikipedia.org/wiki/Aggregatfunktion) anzuwenden sind. Wie bei allen anderen Aufzählungen werden die einzelnen Elemente mit Komma voneinander getrennt.

    Quelle

- Quelle gibt an, wo die Daten herkommen. Es können [Relationen](https://de.wikipedia.org/wiki/Relation_(Datenbank)) und [Sichten](https://de.wikipedia.org/wiki/Sicht_(Datenbank)) angegeben werden und miteinander als [kartesisches Produkt](https://de.wikipedia.org/wiki/Kartesisches_Produkt) oder als Verbund ([JOIN](https://de.wikipedia.org/wiki/Relationale_Algebra#Join), ab SQL-92) verknüpft werden. Mit der zusätzlichen Angabe eines Namens können Relationen für die Abfrage umbenannt werden (vgl. [Beispiele](https://de.wikipedia.org/wiki/SQL#Sprachelemente_und_Beispiele)).
- Where-Klausel bestimmt Bedingungen, auch Filter genannt, unter denen die Daten ausgegeben werden sollen. In SQL ist hier auch die Angabe von Unterabfragen möglich, so dass SQL  wird.

    streng relational vollständig

- Group-by-Attribut legt fest, ob unterschiedliche Werte als einzelne Zeilen ausgegeben werden sollen (GROUP BY = Gruppierung) oder aber die Feldwerte der Zeilen durch Aggregationen wie Addition (SUM), Durchschnitt (AVG), Minimum (MIN), Maximum (MAX) zu einem Ergebniswert zusammengefasst werden, der sich auf die Gruppierung bezieht.
- Having-Klausel ist wie die Where-Klausel, nur dass sich die angegebene Bedingung auf das Ergebnis einer Aggregationsfunktion bezieht, zum Beispiel HAVING SUM (Betrag) > 0.
- Sortierungsattribut: nach ORDER BY werden Attribute angegeben, nach denen sortiert werden soll. Die Standardvoreinstellung ist ASC, das bedeutet aufsteigende Sortierung, DESC ist absteigende Sortierung.

Mengenoperatoren können auf mehrere SELECT-Abfragen angewandt werden, die gleich viele Attribute haben und bei denen die Datentypen der Attribute übereinstimmen:

- UNION vereinigt die Ergebnismengen. In einigen Implementierungen werden mehrfach vorkommende Ergebnistupel wie bei DISTINCT entfernt, ohne dass „UNION DISTINCT“ geschrieben werden muss bzw. darf.
- UNION ALL vereinigt die Ergebnismengen. Mehrfach vorkommende Ergebnistupel bleiben erhalten. Einige Implementierungen interpretieren aber „UNION“ wie „UNION ALL“ und verstehen das „ALL“ möglicherweise nicht und geben eine Fehlermeldung aus.
- EXCEPT liefert die Tupel, die in einer ersten, jedoch nicht in einer zweiten Ergebnismenge enthalten sind. Mehrfach vorkommende Ergebnistupel werden entfernt.
- MINUS ist ein analoger Operator wie EXCEPT, der von manchen SQL-Dialekten alternativ benutzt wird.
- INTERSECT liefert die Schnittmenge zweier Ergebnismengen. Mehrfach vorkommende Ergebnistupel werden entfernt.

### **Einfügen von Datensätzen (INSERT)**

```sql
INSERT INTO Vorlesung (VorlNr, Titel, PersNr) VALUES (1000, 'Softwareentwicklung 1', 12);
INSERT INTO Vorlesung (VorlNr, Titel, PersNr) VALUES (1600, 'Algorithmen', 12);
INSERT INTO Vorlesung (VorlNr, Titel, PersNr) VALUES (1200, 'Netzwerke 1', 20);
INSERT INTO Vorlesung (VorlNr, Titel, PersNr) VALUES (1001, 'Datenbanken', 15);
```

### **Ändern von Datensätzen**

```sql
UPDATE Vorlesung
SET VorlNr = VorlNr + 1000, PersNr = 20
WHERE PersNr = 15;
```

### **Löschen von Datensätzen**

```sql
DELETE FROM Vorlesung
WHERE PersNr = 12;
```

### **Zusammenfassung von INSERT, UPDATE, DELETE**

Verallgemeinert sehen die Änderungsanweisungen so aus:

INSERT-Anweisung:

```sql
INSERT INTO Quelle [(Auswahlliste)]
VALUES (Werteliste) | SELECT <Auswahlkriterien>;
```

UPDATE-Anweisung:

```sql
UPDATE Quelle SET Zuweisungsliste
[FROM From Klausel]
[WHERE Auswahlbedingung];
```

DELETE-Anweisung:

```sql
DELETE FROM Quelle
[WHERE Auswahlbedingung];
```

## Datendefinition

### **Datenbanktabelle**

Die Datenbanktabelle Vorlesung kann mit der folgenden Anweisung erzeugt werden:

```sql
CREATE TABLE Vorlesung (VorlNr INT NOT NULL PRIMARY KEY, 
												Titel VARCHAR NOT NULL, 
												PersNr NOT NULL), 
												FOREIGN KEY (PersNr) 
												REFERENCES Professor (PersNr);
```

In keinem der Felder VorlNr, Titel, PersNr ist der Wert `NULL` erlaubt. Der [Fremdschlüssel](https://de.wikipedia.org/wiki/Fremdschl%C3%BCssel) PersNr referenziert den [Primärschlüssel](https://de.wikipedia.org/wiki/Prim%C3%A4rschl%C3%BCssel) PersNr der Tabelle Professor. Damit wird sichergestellt, dass in die Tabelle Vorlesung nur Datensätze eingefügt werden können, für die der Wert von PersNr in der Tabelle Professor als Primärschlüssel vorkommt (siehe [referenzielle Integrität](https://de.wikipedia.org/wiki/SQL#Referenzielle_Integrit%C3%A4t)).

### **Datenbankindex**

Mit der Anweisung

```sql
CREATE INDEX VorlesungIndex
ON Vorlesung (PersNr, Titel);
```

kann ein [Datenbankindex](https://de.wikipedia.org/wiki/Datenbankindex) für die Tabelle Vorlesung definiert werden, der vom Datenbanksystem bei der Ausführung von Abfragen zur Beschleunigung verwendet werden kann. Ob das sinnvoll ist, entscheidet das Datenbanksystem eigenständig durch komplexe Auswertungen und Analysen für jede Abfrage erneut.

### **Sicht**

Eine [Sicht](https://de.wikipedia.org/wiki/Sicht_(Datenbank)) ist im Wesentlichen ein Alias für eine Datenbankabfrage. Sie kann wie eine Datenbanktabelle verwendet werden. Die Anweisung

```sql
CREATE VIEW Vorlesungssicht AS
SELECT Vorlesung.VorlNr, Vorlesung.Titel, Professor.PersNr, Professor.Name
FROM Professor 
INNER JOIN Vorlesung 
ON Professor.PersNr = Vorlesung.PersNr;
```

speichert die definierte Abfrage als Sicht. Die Abfrage

```sql
SELECT Titel, Name
FROM Vorlesungssicht
WHERE VorlNr < 5000;
```

### **Zusammenfassung**

Zusammengefasst sind die wichtigsten Elemente der Definition einer Datenbanktabelle, eines Datenbankindex oder einer [Sicht](https://de.wikipedia.org/wiki/Sicht_(Datenbank)) wie folgt anzugeben:

```sql
CREATE TABLE Tabellenname (Attributdefinition [PRIMARY KEY]) [, FOREIGN KEY (Attributliste) REFERENCES Tabellenname (Attributliste)]);
DROP TABLE Tabellenname;
ALTER TABLE Tabellenname (Attributdefinition [PRIMARY KEY]) [, FOREIGN KEY (Attributliste) REFERENCES Tabellenname (Attributliste)]);

CREATE INDEX Indexname ON Tabellenname (Attributliste);
DROP INDEX Indexname;

CREATE VIEW Sichtname [(Attributliste)] AS SELECT <Auswahlkriterien>;
DROP VIEW Sichtname;
```

## Normalisierung (Datenbank)

Unter Normalisierung eines relationalen Datenschemas (Tabellenstruktur) versteht man die Aufteilung von Attributen
(Tabellenspalten) in mehrere Relationen (Tabellen) gemäß den Normalisierungsregeln (s. u.), so dass eine Form entsteht, die keine
Redundanzen mehr enthält.

Die Normalisierung hat den Zweck, Redundanzen (mehrfaches Festhalten des gleichen Sachverhalts) zu verringern und dadurch
verursachte Anomalien (z. B. infolge Änderung an nicht allen Stellen) zu verhindern, um so die Aktualisierung einer Datenbank
zu vereinfachen (Änderungen lediglich an einer Stelle) sowie die Konsistenz der Daten zu gewährleisten.

Zurzeit gebräuchliche Normalformen sind:

**1. Normalform (1NF)**

**2. Normalform (2NF)**

**3. Normalform (3NF)**

**Boyce-Codd-Normalform (BCNF)**

**4. Normalform (4NF)**

**5. Normalform (5NF)**

Zum einen dienen sie der Beurteilung der Qualität eines betrachteten Datenbankschemas, zum anderen helfen sie, Fehler beim
Erzeugen neuer Schemata zu vermeiden.

### **Erste Normalform 1NF**

Die erste Normalform bildet die Ausgangsbasis für alle weiteren Normalformen.

Eine Tabelle befindet sich in der ersten Normalform, falls die Wertebereiche der Merkmale atomar (unteilbar->keine Listen) sind.

**Überführungsregel zur 1NF**

Um eine unnormalisierte Tabelle in die erste Normalform zu überführen, muss man:

1. Merkmale, deren Wertebereiche unterschiedliche Informationseinheiten enthalten, auf mehrere Merkmale mit atomaren Wertebereichen aufteilen.
2. Listen sinngleicher Informationseinheiten aus den Wertebereichen der Merkmale entfernen.

**Vorgehensweise zum Entfernen von Listen:**

1. Für jedes Element einer Liste im Wertebereich eines Merkmals muss ein eigener Datensatz in der Tabelle erzeugt werden.
2. Der Schlüssel der Tabelle muss neu bestimmt werden.

### **Zweite Normalform 2NF**

Die zweite Normalform untersucht die volle funktionale Abhängigkeit der Nichtschlüsselmerkmale vom zusammengesetzten Schlüssel.

**Funktionale Abhängigkeit**

Ein Merkmal A ist funktional abhängig von einem Merkmal S, wenn zu jedem möglichen Wert von S genau ein Wert aus A existiert.

**Schreibweise:** S → A

**Volle funktionale Abhängigkeit**

Ein Merkmal A is voll funktional abhängig von einem aus S1 und S2 zusammengesetzten Schlüssel, wenn A funktional abhängig vom Gesamtschlüssel ist, nicht aber von seinen Teilschlüsseln.

**Schreibweise:** (S1, S2) ⇒ A

Schaubild zur vollen funktionalen Abhängigkeit: 

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/60a19acc-bf47-4647-b3e1-1b162add50a5/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/60a19acc-bf47-4647-b3e1-1b162add50a5/Untitled.png)

Eine Tabelle ist in zweiter Normalform, wenn sie die 1NF erfüllt und wenn **alle** Nichtschlüsselmerkmale vom zusammengesetzten Schlüssel voll funktional abhängig sind.

**Überführungsregel zur 2NF**

Eine Tabelle, die der 1NF genügt, aber nicht die 2NF erfüllt, muss in Teiltabellen zerlegt werden. Dabei fasst man alle Merkmale, die von einem Teilschlüssel funktional abhängig sind, und diesen Teilschlüssel zu einer eigenständigen Tabelle zusammen.

**Dieses kann in drei Schritten erfolgen:**

1. Bestimme alle Nichtschlüsselmerkmale, die bereits von einem Teilschlüssel funktional abhängig sind.
2. Bilde aus den Teilschlüsseln und allen von ihnen funktional abhängigen Nichtschlüsselmerkmalen eigene Tabellen.
3. Entferne aus der ursprünglichen Tabelle alle nicht voll funktional abhängigen Nichtschlüsselmerkmale.

### **Dritte Normalform 3NF**

Die dritte Normalform stellt sicher, dass es keine transitiv abhängigen Nichtschlüsselmerkmale in einer Tabelle geben kann.

**Transitivität**

Wenn man aus "S bestimmt A" und "A bestimmt B" folgern kann, dass zwangsläufig auch "S bestimmt B" gilt, dann ist die Transitivität gegeben.

**Transitive Abhängigkeit**

Ein Merkmal B ist transitiv abhängig von einem Merkmal S, wenn es ein Merkmal A gibt, so dass gilt:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8aae7072-8578-418c-bf15-6d58d1730a25/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8aae7072-8578-418c-bf15-6d58d1730a25/Untitled.png)

Schaubild zur transitiven Abhängigkeit:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f6b8fa1a-f42c-4755-8b40-e4e35f223a7c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f6b8fa1a-f42c-4755-8b40-e4e35f223a7c/Untitled.png)

### **Dritte Normalform (3NF)**

Eine Tabelle befindet sich in dritter Normalform, wenn sie die 2NF erfüllt und **kein** Nichtschlüsselmerkmal vom Schlüssel transitiv abhängig ist.

**Überführungsregel zur 3NF**

Eine Tabelle, die der 1NF und der 2NF genügt, aber nicht die 3NF erfüllt, muss in Teiltabellen zerlegt werden. Dabei müssen alle vom Schlüssel transitiv abhängigen Nichtschlüsselmerkmale zusammen mit den Nichtschlüsselmerkmalen, von denen sie funktional abhängig sind, zu eigenen Tabellen zusammengefasst werden.

**Dieses kann in drei Schritten erfolgen:**

1. Bestimme alle vom Schlüssel transitiv abhängigen Nichtschlüsselmerkmale.
2. Bilde aus diesen transitiv abhängigen Nichtschlüsselmerkmalen, von denen sie funktional abhängig sind, eigene Tabellen.
3. Entferne aus der ursprünglichen Tabelle alle transitiv abhängigen Nichtschlüsselmerkmale.

**Anmerkung**

Mitunter kommt es vor, dass aus Gründen der Praktikabilität auf die strikte Umsetzung der 3NF verzichtet wird. Beispielsweise ist es nicht in jedem Fall sinnvoll, die Information "Postleitzahl" und "Ort" durch eine eigenen Orts-Tabelle umzusetzen, sondern sie als Merkmale einer Entität anzusehen.

## SQL-Datentypen

In den oben vorgestellten Befehlen `create table` und `alter table` wird bei der Definition jeder Spalte angegeben, welchen Datentyp die Werte dieser Spalte annehmen können. 

Dazu liefert SQL eine ganze Reihe standardisierter Datentypen mit. Die einzelnen DBMS-Hersteller haben diese Liste jedoch um eine Unzahl weiterer Datentypen erweitert. Die wichtigsten Standarddatentypen sind:

**`integer`**

[Ganze Zahl](https://de.wikipedia.org/wiki/Ganze_Zahl) (positiv oder negativ), wobei je nach Zahl der verwendeten Bits Bezeichnungen wie smallint, tinyint oder bigint verwendet werden. Die jeweiligen Grenzen und die verwendete Terminologie sind vom Datenbanksystem definiert.

**`numeric (n, m)` oder `decimal (n, m)`**

[Festkommazahl](https://de.wikipedia.org/wiki/Festkommazahl) (positiv oder negativ) mit insgesamt maximal `n` Stellen, davon `m` Nachkommastellen. Wegen der hier erfolgenden Speicherung als Dezimalzahl ist eine besonders für Geldbeträge notwendige Genauigkeit gegeben.

**`float (m)`**

[Gleitkommazahl](https://de.wikipedia.org/wiki/Gleitkommazahl) (positiv oder negativ) mit maximal `m` Nachkommastellen.**`real`**Gleitkommazahl (positiv oder negativ). Die Genauigkeit für diesen Datentyp ist jeweils vom Datenbanksystem definiert.

**`double` oder `double precision`**

Gleitkommazahl (positiv oder negativ). Die Genauigkeit für diesen Datentyp ist jeweils vom Datenbanksystem definiert.

**`float` und `double`**

sind für technisch-wissenschaftliche Werte geeignet und umfassen auch die Exponentialdarstellung. Wegen der Speicherung im Binärformat sind sie aber für Geldbeträge nicht geeignet, weil sich beispielsweise der Wert 0,10 € (entspricht 10 Cent) nicht exakt abbilden lässt.

**`character (n)` oder `char (n)`**

Zeichenkette Text mit `n` Zeichen.

**`varchar (n)` oder `character varying (n)`**

Zeichenkette (also Text) von variabler Länge, aber maximal `n` druckbaren und/oder nicht druckbaren Zeichen. Die Variante `varchar2` ist für Oracle spezifisch, ohne dass sie sich tatsächlich unterscheidet.

**`text`**

Zeichenkette (zumindest theoretisch) beliebiger Länge. In manchen Systemen synonym zu `clob`.

**`date`**

Datum (ohne Zeitangabe)

**`time`**

Zeitangabe (evtl. inklusive Zeitzone)

**`timestamp`**

Zeitstempel (umfasst Datum und Uhrzeit; evtl. inklusive Zeitzone), meistens mit Millisekundenauflösung, teilweise auch mikrosekundengenau

**`boolean`**

Boolesche Variable (kann die Werte `true`(wahr) oder `false` (falsch) oder `NULL` (unbekannt) annehmen). Dieser Datentyp ist laut SQL:2003 optional und nicht alle DBMS stellen diesen Datentyp bereit.

**`[blob](https://de.wikipedia.org/wiki/Binary_Large_Object) (n)` oder `binary large object (n)`**

Binärdaten von maximal `n` Bytes Länge.

**`[clob](https://de.wikipedia.org/wiki/Character_Large_Object) (n)` oder `character large object (n)`**

Zeichenketten mit maximal `n` Zeichen Länge.

Wenn es die Tabellendefinition erlaubt, können Attribute auch den Wert `NULL` annehmen, wenn kein Wert bekannt ist oder aus anderen Gründen kein Wert gespeichert werden soll. 

Der `NULL`Wert ist von allen anderen möglichen Werten des Datentyps verschieden.
