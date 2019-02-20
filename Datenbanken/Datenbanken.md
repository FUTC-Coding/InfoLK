# Datenbanken

## Tabellenform

![2019-02-20 18-10-34-1](E:\nextcloud\Info lk\Lernzettel\Datenbanken\2019-02-20 18-10-34-1.png)

Als Schema:

Buch(<u>ISBN</u>, Titel, Autor, Preis)

**Redundanz**: Eine Redundanz liegt vor, wenn Daten mehrmals gespeichert werden, Sie können weggelassen werden, ohne dass Informationen verloren gehen.



**Anomalien**: Sind Probleme und Fehler, die bei Operationen auf den Datensätzen einer Datenbank entstehen können. Es werden Änderungs-,Einfüge- und Löschanomalien unterschieden.

**Inkonsistenzen**: Sind Wiedersprüche im Datenbestand einer Datenbank. Sie können durch Anomalien hervorgerufen werden.

**Projektion**: Die Projektion wird in SQL in der SELECT-Klausel kodiert. 

​			Beispiel: `SELECT Name, Preis FROM Produkte`

**Selektion**: In der WHERE-Klausel kodiert.

​			Beispiel: `SELECT * FROM Produkte WHERE Preis > 5`

## Kardinalitäten

Kardinalitäten beschreiben wie viele Entitäten einer Entitätsmenge and einer konkreten Beziehung beteiligt sein können oder müssen. Es werden die Kardinalitäten

- 1 (kein oder ein)
- m bzw. n (kein, ein, oder mehrere)

unterschieden. Damit sind drei Beziehungsarten möglich:

- 1:1
- 1:n
- m:n

## ER-Modell

![ER-Modell](E:\nextcloud\Info lk\Lernzettel\Datenbanken\ER-Modell.png)

## ER-Modell -> Tabellen

**Regel 1**: Jede Entitätsmenge wird im relationalen Modell in eine eigenständige Relation überführt.

​		**z.B.:** Buch(<u>ISBN</u>, Titel, Autor, Preis, Kategorie)

**Regel 2**: Jede n:m-Beziehung wird im relationalen Modell in eine eigenständige Relation überführt.

​		**z.B.:** bestellt(<u>↑ISBN</u>, <u>↑Benutzername</u>, Anzahl)

**1:n - Beziehung**: Die Relation "Buch" kann die Beziehung zum jeweiligen Verlag aufnehmen. Dies geschieht indem der Primärschlüssel **VID** der Relation der Relation Verlag als Fremdschlüssel der Relation Buch angefügt wird.

​		Buch(<u>ISBN</u>, Titel, Autor, Preis, ↑VID)

**Regel 3**: Jede 1:n - Beziehung wird im relationalen Modell ohne eine eigene Tabelle abgebildet. Dies geschieht, indem der Relation mit der Kardinalität n der Primärschlüssel der Relation mit der Kardinalität 1 als Fremdschlüssel angefügt wird. Attribute der Beziehungsmenge werden ggf. auch dieser Relation angefügt.

**Regel 4**: Jede 1:1 - Beziehung wird im relationalen Modell ohne eine eigene Tabelle abgebildet. Dies geschieht, indem einer der an der Beziehung beteiligten Relationen der Primärschlüssel der anderen Relation als Fremdschlüssel angefügt wird. Attribute der Beziehungsmenge werden ggf. auch dieser Relation angefügt.

​		**z.B.:** Darstellung(<u>DID</u>, d_Bewertungen, lieferbar, ↑ISBN)



Verlag(<u>VID</u>, Name, Sitz, Ansprechpartner)

Buch(<u>ISBN</u>, Titel, Autor, Preis, Kategorie, ↑VID) **Umsetzung der 1:n - Beziehung**

Kunde(<u>Benutzername</u>, [...])

Darstellung(<u>DID</u>, d_Bewertung, lieferbar, ↑ISBN) **Umsetzung der 1:1 - Beziehung**

bestellt(<u>↑ISBN</u>, <u>↑Benutzername</u>, Anzahl) **Umsetzung der n:m - Beziehung**

## Integritätsbedingungen

**1. Datenfeldebene:** Jedem Datenfeld wird ein bestimmter Wertebereich zugewiesen, man kann nicht willkürlich Daten eintragen.

**2. Datensatzebene:** Jeder Datensatz muss über den Primärschlüssel eindeutig identifizierbar sein.

**3. Beziehungsebene:** Beziehungen werden im relationalen Modell durch Fremdschlüssel realisiert. Wird der Datensatz gelöscht auf den der Fremdschlüssel verweist, entsteht eine inkonsistente Referenz, die Kontrolle der referenziellen Integrität soll solche inkonsistenten Referenzen verhindern.



Das DBMS sollte im Fall des Löschens eines Primärschlüssels eine referenzielle Integrität mit Löschweitergabe umsetzen. Aber manchmal muss das DBMS das Löschen verhindern weil sonst zu viel gelöscht wird.

## Normalformen

### Erste Normalform

Die Attribute werden atomisiert. Das Attribut `Name` wird z.B. zu den Attributen `Vorname` & `Nachname`.

### Zweite Normalform

Ein Attribut B ist von einem Attribut A **funktional abhängig** wenn durch jeden Wert von A eindeutig ein Wert für B bestimmt wird. A → B

Ein Attribut B ist von einer Attributkombination (A1, A2) **voll funktional abhängig**, wenn B abhängig von der Kombination ist nicht aber Bereits von A1 oder A2.

Für die Zweite Normalform werden die Attribute ihrer Abhängigkeit nach in andere Tabellen eingelagert.

Ein Datenbankschema ist in der zweiten Normalform, wenn es in der 1NF ist und zusätzlich jedes Nichtschlüsselattribut vom Primärschlüssel voll funktional abhängig ist und nicht bereits von einem Teil der Schlüsselattribute..

### Dritte Normalform

Ein Attribut C ist von einem Attribut A **transitiv abhängig**, wenn es ein Attribut B gibt mit A→B→C. Dabei darf A nicht funktional abhängig sein von B.

Ein Datenbankschema ist in der 3NF wenn es in der 2NF ist und zusätzlich kein Nichtschlüsselattribut gibt, dass transitiv abhängig von einem Schlüsselattribut ist. Es darf also keine funktionalen Abhängigkeiten zwischen Nichtschlüsselattributen geben.