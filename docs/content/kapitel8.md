# Kapitel 8 – Dateien, CSV & JSON

<div class="kurs-progress">
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step active"></div>
  <div class="step"></div>
  <div class="step"></div>
</div>

<div class="lernziele" markdown>
<h3>Was du in diesem Kapitel lernst</h3>

- Textdateien lesen und schreiben mit `open()` und `with`
- Warum `with` die sichere Art ist, Dateien zu öffnen
- CSV-Dateien (Tabellen) mit dem `csv`-Modul verarbeiten
- JSON-Daten lesen und speichern
- Die häufigsten Datei-Fehler erkennen und vermeiden
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Neues Thema</span>
**Dieses Kapitel ist neu** – Dateien, CSV und JSON kamen im ersten Kursteil noch nicht vor. Voraussetzung sind Schleifen (Kapitel 6) und Funktionen/Module (Kapitel 7).
</div>

## So gehst du vor

1. Lege dir zum Üben kleine Testdateien **im selben Ordner** wie dein Skript an.
2. Nutze **immer** `with open(...)` – das erspart dir Fehler.
3. Bearbeite die **Kurzübungen**.

---

## 8.1 Eine Datei lesen

```python
with open("beispiel.txt", "r", encoding="utf-8") as datei:
    inhalt = datei.read()
    print(inhalt)
```

Drei Bausteine:

- **`open("beispiel.txt", "r", ...)`** öffnet die Datei zum Lesen (`"r"` = read).
- **`encoding="utf-8"`** sorgt dafür, dass Umlaute (ä, ö, ü) korrekt gelesen werden.
- **`with`** schließt die Datei automatisch wieder – auch wenn unterwegs ein Fehler passiert.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `with open("datei.txt") as f:` | `$f = fopen("datei.txt", "r");` … `fclose($f);` |
    | `inhalt = f.read()` | `$inhalt = file_get_contents("datei.txt");` |
    | `"r"` / `"w"` / `"a"` | `"r"` / `"w"` / `"a"` (gleiche Idee) |

    `with` schließt die Datei **automatisch** – in PHP musst du `fclose()` nicht vergessen.

### Die Öffnungs-Modi

| Modus | Bedeutung | Achtung |
|---|---|---|
| `"r"` | Lesen (read) | Datei muss existieren |
| `"w"` | Schreiben (write) | **überschreibt** vorhandenen Inhalt komplett! |
| `"a"` | Anhängen (append) | hängt ans Ende an, vorhandenes bleibt |

!!! warning "Stolperstein: `\"w\"` löscht den Inhalt"
    Öffnest du eine bestehende Datei mit `"w"`, ist ihr alter Inhalt **sofort weg** – noch bevor du etwas geschrieben hast. Willst du etwas ergänzen, nimm `"a"`.

---

## 8.2 Eine Datei schreiben

```python
with open("ausgabe.txt", "w", encoding="utf-8") as datei:
    datei.write("Zeile 1\n")
    datei.write("Zeile 2\n")
```

`\n` ist der **Zeilenumbruch**. Ohne ihn landet alles in einer Zeile. Anders als `print()` fügt `write()` **keinen** automatischen Umbruch hinzu.

---

## 8.3 Zeile für Zeile lesen

Große Dateien liest man nicht auf einmal, sondern Zeile für Zeile in einer Schleife:

```python
with open("beispiel.txt", "r", encoding="utf-8") as datei:
    for zeile in datei:
        print(zeile.strip())
```

`.strip()` entfernt den Zeilenumbruch (und Leerzeichen) am Anfang und Ende – sonst hättest du doppelte Leerzeilen.

!!! warning "Häufigster Datei-Fehler: Datei nicht gefunden"
    ```
    FileNotFoundError: [Errno 2] No such file or directory: 'beispiel.txt'
    ```

    → Die Datei liegt nicht dort, wo das Skript sucht. Ursachen: Tippfehler im Namen, oder das Terminal läuft in einem anderen Ordner. Prüfe mit `import os; print(os.getcwd())`, **wo** Python gerade sucht, und lege die Datei dort ab.

---

## 8.4 CSV-Dateien (Tabellen)

**CSV** (Comma-Separated Values) ist das Standardformat für Tabellen – z. B. Export aus Excel. Jede Zeile ist ein Datensatz, die Spalten sind durch Kommas getrennt.

**`noten.csv`:**

```csv
Name,Note
Anna,2
Bob,3
Charlie,1
```

### CSV lesen

```python
import csv

with open("noten.csv", "r", encoding="utf-8") as datei:
    reader = csv.DictReader(datei)
    for row in reader:
        print(f"{row['Name']}: Note {row['Note']}")
```

**Ausgabe:**

```
Anna: Note 2
Bob: Note 3
Charlie: Note 1
```

`csv.DictReader` nimmt die **erste Zeile als Spaltennamen** und liefert jede weitere Zeile als „Wörterbuch", auf das du per Spaltenname zugreifst (`row['Name']`).

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `csv.DictReader` + `row['Name']` | `fgetcsv()` – oft mit `$row[0]` statt Spaltenname |
    | Kopfzeile wird automatisch Spaltenname | Spaltennamen musst du selbst auswerten |

    `DictReader` spart dir die manuelle Zuordnung von Spaltenindex → Name.

### CSV schreiben

```python
import csv

daten = [
    {"Name": "Anna", "Note": "2"},
    {"Name": "Bob", "Note": "3"},
]

with open("noten_neu.csv", "w", encoding="utf-8", newline="") as datei:
    writer = csv.DictWriter(datei, fieldnames=["Name", "Note"])
    writer.writeheader()
    writer.writerows(daten)
```

!!! warning "Stolperstein: `newline=\"\"` beim Schreiben"
    Beim CSV-**Schreiben** gehört `newline=""` in den `open`-Aufruf. Lässt du es weg, entstehen unter Windows **leere Zwischenzeilen**. Einfach immer mitschreiben.

---

## 8.5 JSON-Dateien

**JSON** ist das Standardformat für **strukturierte** Daten (Konfigurationen, APIs). Es sieht fast aus wie Python selbst.

**`config.json`:**

```json
{
  "kurs": "Vorkurs Programmierung",
  "tage": 5,
  "aktiv": true
}
```

### JSON lesen und schreiben

```python
import json

# Lesen: JSON-Datei → Python-Daten
with open("config.json", "r", encoding="utf-8") as datei:
    config = json.load(datei)

print(config["kurs"])   # Vorkurs Programmierung
print(config["tage"])   # 5

# Verändern und wieder speichern
config["tage"] = 6
with open("config.json", "w", encoding="utf-8") as datei:
    json.dump(config, datei, indent=2, ensure_ascii=False)
```

| Funktion | Richtung | Merke |
|---|---|---|
| `json.load(datei)` | Datei → Python | „load = laden" |
| `json.dump(daten, datei)` | Python → Datei | „dump = ablegen" |

- **`indent=2`** macht die Datei schön eingerückt und lesbar.
- **`ensure_ascii=False`** sorgt dafür, dass Umlaute als ä/ö/ü gespeichert werden statt als `\u00e4`.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `json.load(datei)` | `json_decode(file_get_contents(...))` |
    | `json.dump(daten, datei)` | `file_put_contents(..., json_encode($daten))` |
    | JSON-Objekt → `dict` | JSON-Objekt → assoziatives Array |

    Zugriff auf Felder: `config["kurs"]` in Python, `$config['kurs']` in PHP.

!!! warning "Häufiger JSON-Fehler"
    ```
    json.decoder.JSONDecodeError: Expecting ',' delimiter ...
    ```

    → Die JSON-Datei ist fehlerhaft (fehlendes Komma, einfache statt doppelter Anführungszeichen, Komma hinter dem letzten Eintrag). JSON verlangt **doppelte** Anführungszeichen und **kein** Komma nach dem letzten Element.

---

## 8.6 Pfade richtig handhaben

```python
import os

print(os.getcwd())                  # In welchem Ordner läuft das Skript?
print(os.path.exists("noten.csv"))  # Existiert die Datei? True/False
```

!!! tip "Relative Pfade sind am einfachsten"
    Lege Testdateien in **denselben Ordner** wie dein Skript und sprich sie nur über den Dateinamen an (`"noten.csv"`). Starte das Skript aus diesem Ordner. Absolute Pfade (`C:\Users\...`) funktionieren auf jedem Rechner anders – für den Anfang vermeiden.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `os.getcwd()` | `getcwd()` |
    | `os.path.exists("datei.csv")` | `file_exists("datei.csv")` |
    | `os.path.join(ordner, datei)` | `$ordner . DIRECTORY_SEPARATOR . $datei` |

    `os.path.join()` baut Pfade **plattformunabhängig** zusammen – unter Windows und Linux korrekt.

---

## Kurzübungen

{{ task(file="tasks/tag8_01.yaml") }}

{{ task(file="tasks/tag8_02.yaml") }}

{{ task(file="tasks/tag8_03.yaml") }}
