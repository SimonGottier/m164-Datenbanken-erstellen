# m164-Datenbanken-erstellen

## 18.02.25:
Ich habe nach der Moduleinführung damit begonnen MYSQL mithilfe von XAMPP zu installieren. Jedoch hat dies bei mir nicht richtig funktioniert. Ich weiss nicht woran das lag. Danach habe ich mich auf den 1. Auftrag konzentriert und ein ERM dafür entworfen:
(Bild Einfügen)

## 25.02.25: 
Nun hat die Installalation von XAMPP geklappt und ich konnte Apache und mySQL im XAMPP Controller starten. Danach habe ich damit begonnen mit der MY SL Workbench eine DB zu erstellen: (Bild einfügen)

## 04.03.25:
Heute habe ich viel über beziehungen inner und asserhalb (zwischen) Tabellen gelernt. 
Mehrfachbeziehungen zwischen Tabellen: Zwei Tabellen (z. B. tbl_Fahrten und tbl_Orte) können mehrere, voneinander unabhängige Beziehungen haben, die unterschiedliche Sachverhalte abbilden. Jede Beziehung sollte eindeutig und verständlich benannt werden. Die Kardinalitäten dieser Beziehungen können unterschiedlich sein. Bei m:n-Beziehungen (z. B. Orte, die bei einer Tour angefahren werden) ist eine Zwischentabelle nötig.

Selbstbeziehungen innerhalb einer Tabelle: Ein Datensatz kann sich auf einen anderen Datensatz derselben Tabelle beziehen, z. B. in hierarchischen Strukturen wie Firmenorganisationen (eine Person hat eine andere als Vorgesetzten). Diese Beziehung wird durch einen Fremdschlüssel gelöst, der auf den Primärschlüssel derselben Tabelle verweist. Damit auch die oberste Hierarchieebene (ohne Vorgesetzten) abgebildet werden kann, darf dieser Fremdschlüssel nicht zwingend (also nicht „Not Null“) sein.

## 11.03.25
Heute hatten wir zuerst die LB1. Danach habe ich an den Aufträgen gearbeitet: 
Zuerst habe ich die Datei BeziehungenLE.mwb von der angegebenen Quelle heruntergeladen.

Anschließend habe ich die Datei mit MySQL Workbench geöffnet.

Im geöffneten Modell habe ich das ER-Diagramm (ERD) analysiert, um einen Überblick über die enthaltenen Tabellen und Beziehungen zu erhalten.

Danach bin ich in die Einstellungen gegangen (Edit > Preferences > Modeling > Diagram) und habe dort das Häkchen bei "Show Caption" gesetzt, um die Beziehungsnamen sichtbar zu machen.

Ich habe mir die vier geforderten Beziehungstypen angeschaut: 1:1, 1:n, m:n und rekursive Beziehung.

Für jede Beziehung habe ich geprüft, welche Tabellen beteiligt sind und welche Rolle die Fremdschlüssel spielen.

Dann habe ich im Modell die Beziehungen Schritt für Schritt erstellt, jeweils über "Place a Relationship Using Existing Columns".

Für jede Beziehung habe ich die passenden Kardinalitäten definiert, damit z. B. m:n-Beziehungen korrekt mit einer Zwischentabelle dargestellt werden.

In den Spalteneigenschaften der Fremdschlüssel habe ich jeweils die Constraints gesetzt: NN (Not Null) oder UQ (Unique) – je nachdem, was laut Vorgabe erforderlich war.

Besonders bei der 1:1-Beziehung habe ich auf Unique beim Fremdschlüssel geachtet, damit die Eindeutigkeit sichergestellt ist.

Die rekursive Beziehung habe ich innerhalb einer Tabelle angelegt, indem ich einen Fremdschlüssel auf den eigenen Primärschlüssel gesetzt habe.

Danach habe ich noch einmal das gesamte Modell kontrolliert, um sicherzustellen, dass alle Beziehungen korrekt umgesetzt und benannt waren.

Über das Menü Database > Forward Engineer habe ich anschließend das SQL-Skript generieren lassen.

Dabei habe ich alle relevanten Optionen aktiviert (wie z. B. Foreign Keys, Engine, etc.), um ein vollständiges DDL-Skript zu erhalten.

Schließlich habe ich das erzeugte DDL-SQL-Script gespeichert, um es bei Bedarf in einer Datenbankumgebung ausführen zu können.

## 18.03.25:
Wir haben heute Theorie gehört und diese in Aufträgen umgesetzt.
In professionellen Datenbanken können Daten nicht einfach so gelöscht werden, weil dadurch die referentielle Integrität verletzt werden könnte. Das bedeutet: Wenn ein Datensatz in einer Tabelle gelöscht wird, auf den in einer anderen Tabelle noch verwiesen wird (z. B. über einen Fremdschlüssel), entsteht ein inkonsistenter Zustand – die Daten verweisen auf etwas, das es nicht mehr gibt.

Gründe, warum das Löschen eingeschränkt ist:
Verwaiste Datensätze vermeiden: Fremdschlüsselbeziehungen sorgen dafür, dass abhängige Daten nicht ins Leere zeigen.

Datenkonsistenz: Alle Daten sollen logisch zusammenpassen – das wird durch Regeln erzwungen.

Revisionssicherheit und Nachvollziehbarkeit: Gelöschte Daten könnten für rechtliche oder geschäftliche Zwecke noch relevant sein.

Abhängigkeiten im Geschäftsprozess: Ein gelöschter Kunde könnte z. B. noch Rechnungen oder Verträge haben.

Wer stellt die referentielle Integrität sicher?
Die Datenbankmanagementsysteme (DBMS) wie MySQL, PostgreSQL, Oracle oder SQL Server stellen die referentielle Integrität technisch sicher – über definierte Fremdschlüssel-Constraints. Diese prüfen automatisch beim Einfügen, Aktualisieren oder Löschen, ob die referenzielle Beziehung gültig bleibt.

## 25.03.25: 

Feststellung beim Löschversuch von „4000 Basel“ in tbl_ort
Als Datenbank-Entwickler versuche ich, den Eintrag „4000 Basel“ in der Tabelle tbl_ort zu löschen, da fälschlich statt „3000 Bern“ eingegeben wurde.
Beim Versuch, den Datensatz zu löschen, meldet das Datenbankmanagementsystem (DBMS) jedoch einen Fehler oder verweigert den Löschvorgang.

Warum?
Die Ortschaft „Basel“ ist vermutlich über einen Fremdschlüssel mit anderen Tabellen verknüpft – z. B. tbl_fahrten, tbl_personen oder anderen, die auf tbl_ort referenzieren.
Das Löschen würde also die referentielle Integrität verletzen, da noch andere Datensätze auf diesen Ort verweisen.

Lösungsplan: So kann ich die falsche Ortschaft korrigieren
Überprüfen, in welchen Tabellen die Ortschaft „Basel“ verwendet wird – z. B. durch JOINs oder SELECTs auf tbl_fahrten, tbl_personen etc.

Alle betroffenen Datensätze aktualisieren, sodass sie nicht mehr auf „Basel“ (PLZ 4000), sondern auf „Bern“ (PLZ 3000) verweisen:

Falls „3000 Bern“ noch nicht existiert, zuerst neu in tbl_ort einfügen.

Danach kann ich in den betroffenen Tabellen die Fremdschlüssel von „4000 Basel“ auf „3000 Bern“ umstellen.

Nun ist „Basel“ nicht mehr referenziert – der Datensatz kann gefahrlos gelöscht werden.

Abschließend kann ich optional überprüfen, ob alle Änderungen korrekt umgesetzt wurden.
Ich habe vereinfachten SQL code geschrieben:
-- 1. Neue Ortschaft einfügen, falls nicht vorhanden
INSERT INTO tbl_ort (plz, ortsname)
VALUES (3000, 'Bern')
ON DUPLICATE KEY UPDATE ortsname = 'Bern';

-- 2. Fremdschlüsselbeziehungen aktualisieren (z. B. in tbl_personen)
UPDATE tbl_personen
SET ort_plz = 3000
WHERE ort_plz = 4000;

-- 3. Basel löschen (nun referenzfrei)
DELETE FROM tbl_ort
WHERE plz = 4000;

## 01.04.25 :
Heute haben wir uns auf BAckups konzentriert. So bin ich vorgegangen.
Ich habe MySQL Workbench geöffnet und mich mit dem gewünschten Datenbankserver verbunden.

Nach dem erfolgreichen Verbindungsaufbau habe ich auf der Startseite den Punkt "Data Export" im linken Menü unter „Management“ ausgewählt.

Dort habe ich die Datenbank angehakt, von der ich ein Backup erstellen wollte.

Anschließend habe ich entschieden, ob ich das komplette Datenbankschema, nur bestimmte Tabellen oder zusätzlich die Daten (INSERTs) exportieren möchte.

Ich habe die Option "Export to Self-Contained File" gewählt, um alle Inhalte in eine einzelne .sql-Datei zu schreiben.

Den Speicherort habe ich auf meinem Rechner definiert, zum Beispiel auf dem Desktop oder in einem Projektordner.

Zusätzlich habe ich unter „Advanced Options“ eingestellt, dass DROP TABLE IF EXISTS eingefügt werden soll, damit alte Versionen beim Import entfernt werden.

Ich habe sichergestellt, dass sowohl Struktur als auch Daten exportiert werden (Häkchen bei beidem gesetzt).

Danach habe ich auf "Start Export" geklickt.

Während des Exportvorgangs zeigte mir Workbench unten ein Fortschrittsfenster mit dem Exportstatus an.

Der Vorgang dauerte je nach Datenmenge nur wenige Sekunden.

Nach erfolgreichem Abschluss wurde eine Meldung angezeigt, dass der Export erfolgreich war.

Ich habe zur Kontrolle die erzeugte .sql-Datei geöffnet und den Inhalt geprüft.

Dabei habe ich sichergestellt, dass alle CREATE- und INSERT-Befehle korrekt generiert wurden.

Nun war mein Backup vollständig erstellt und bereit für die Archivierung oder einen späteren Import.

## 08.04.25:
Ich habe den Auftrag wie folgt gelöst: 
Zuerst habe ich die gegebene Excel-Tabelle analysiert und in die 1. Normalform (1NF) überführt, indem ich atomare Felder sichergestellt und mehrwertige Attribute aufgespalten habe.

Anschließend habe ich die Daten in separaten Tabellen organisiert, wobei Redundanzen bewusst in Kauf genommen wurden, um sie später gezielt zu bereinigen.

Ich habe die bereinigten Daten aus Excel als CSV-Dateien exportiert, eine Datei pro logischer Tabelle.

Danach habe ich ein logisches ER-Diagramm (ERD) mit fünf Tabellen erstellt, die mindestens in der 2. Normalform (2NF) waren – also ohne funktionale Abhängigkeiten von Teilschlüsseln.

In diesem ERD habe ich für jede Beziehung die Kardinalitäten bestimmt (z. B. 1:n oder m:n), um die logischen Abhängigkeiten zwischen den Entitäten korrekt darzustellen.

Anschließend habe ich ein physisches ERD in MySQL Workbench erstellt und bei jedem Attribut die nötigen Constraints (NOT NULL, UNIQUE) sowie Fremdschlüsseldefinitionen gesetzt.

Mittels Forward Engineering habe ich das SQL-DDL-Skript erzeugt, das alle Tabellen inklusive Datentypen, Schlüsselbeziehungen und Constraint-Optionen enthielt.

Mit dem Befehl LOAD DATA LOCAL INFILE habe ich die Daten aus den CSV-Dateien in die normalisierten Tabellen geladen.

Ich habe besonders darauf geachtet, dass beim Laden die Fremdschlüssel korrekt zugewiesen wurden (z. B. durch passende ID-Zuordnung).

Anschließend habe ich die Tabellen auf Redundanzen, leere Werte und Inkonsistenzen geprüft und bereinigt, unter Verwendung vorhandener Skriptvorlagen.

Ich habe Test-SELECT-Abfragen formuliert, um die eingelesenen Daten mit den Originalwerten aus den CSV-Dateien zu vergleichen – beide Ergebnisse stimmten überein.

Dann habe ich mit einem Testdatengenerator 290 zusätzliche Schüler:innen-Datensätze erstellt, diese in Excel vorbereitet und erneut als CSV-Dateien gespeichert.

Die zusätzlichen Datensätze habe ich wie zuvor über LOAD DATA eingelesen, die Beziehungen kontrolliert und die Tabellenstruktur bei Bedarf angepasst.

Die gewünschten SELECT-Abfragen (z. B. Teilnehmerzahl bei Inge Sommer, Schüler:innen im Freifach "Chor" oder "Elektronik") habe ich erfolgreich ausgeführt und getestet.

Schließlich habe ich die Ausgaben mit SELECT ... INTO OUTFILE in Textdateien exportiert und ein vollständiges Backup der Datenbank Freifaecher mit MySQL Workbench erstellt.

## 15.04.25:
Heute hatten wir die 2. LB. Der Theorieteil, fiel mir dabei leider sehr schwer, aber ich konnte in der Praxis alles umsetzten und das gelernte aus den Aufträgen nutzen.

## 06.05.25:
Heute habe ich noch einen sehr interessanten auftrag gelöst. Um den inhalt festzuhalten habe ich Ihn zusammengefasst:
Stored Procedures sind gespeicherte SQL-Befehlsfolgen, die direkt in der Datenbank definiert und ausgeführt werden.

Sie dienen dazu, wiederkehrende Aufgaben zu automatisieren und den SQL-Code wiederverwendbar zu machen.

Eine Stored Procedure wird einmal erstellt und kann dann beliebig oft mit einem einfachen Aufruf verwendet werden.

Der Code muss nicht jedes Mal neu geschrieben werden, was Zeit spart und Fehler reduziert.

Die Logik wird zentral in der Datenbank verwaltet, was besonders bei größeren Anwendungen Vorteile bringt.

Stored Procedures verbessern häufig die Performance, da sie direkt auf der Datenbank laufen und nicht über das Netzwerk übertragen werden müssen.

Sie eignen sich gut zur Kapselung komplexer Geschäftsregeln innerhalb der Datenbank.

Die Sicherheit wird erhöht, da Benutzer Prozeduren nutzen können, ohne direkten Zugriff auf Tabellen zu haben.

So lassen sich z. B. sensible Daten schützen, indem nur kontrollierte Aktionen erlaubt sind.

In vielen Datenbanksystemen wie MySQL, SQL Server oder PostgreSQL ist die Verwendung von Stored Procedures möglich.

Die grundlegende Struktur besteht aus einer Definition mit einem Namen, optionalen Parametern, und einem BEGIN...END-Block mit SQL-Befehlen.

Einfache Prozeduren können ohne Parameter definiert werden, komplexere können Ein- und Ausgabeparameter verwenden.

Der genaue Syntaxaufbau variiert je nach verwendetem Datenbankmanagementsystem.

Ein Beispiel für MySQL:

sql
Kopieren
Bearbeiten
DELIMITER //  
CREATE PROCEDURE BeispielProzedur()  
BEGIN  
  SELECT * FROM tbl_personen;  
END //  
DELIMITER ;  
Stored Procedures sind ein mächtiges Werkzeug für saubere, sichere und performante Datenbankanwendungen.
