# Kapitel 9 – Mini-Automationen

<div class="kurs-progress">
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step active"></div>
  <div class="step"></div>
</div>

<div class="lernziele" markdown>
<h3>Was du in diesem Kapitel lernst</h3>

- Was eine Automation ist und wann sie sich lohnt
- Ein kleines Skript von der Idee bis zur Ausführung planen
- Dateien automatisch sortieren, Logdateien auswerten, CSV zusammenfassen
- Alle bisherigen Bausteine (Schleifen, Bedingungen, Funktionen, Dateien) kombinieren
- Automationen sicher testen, ohne echte Daten zu gefährden
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Neues Thema – der Abschluss</span>
**Auch dieses Kapitel ist neu** und bildet das **Ziel des Vorkurses**: aus den bisherigen Bausteinen ein nützliches kleines Programm bauen. Hier kommt alles zusammen – Schleifen, Bedingungen, Funktionen, Dateien und Dictionaries.
</div>

## So gehst du vor

1. Such dir **ein konkretes Problem** – lieber klein und fertig als groß und unvollendet.
2. Plane erst **Input → Verarbeitung → Output**, dann tippe.
3. Teste **immer zuerst mit Kopien/Dummy-Dateien**.
4. Bearbeite die **Kurzübungen**.

---

## 9.1 Was ist eine Automation?

Eine **Automation** ist ein Skript, das eine Aufgabe übernimmt, die du sonst von Hand machst – **schneller, fehlerfreier und beliebig wiederholbar**.

Typische Einstiegs-Automationen:

| Aufgabe | Welche Bausteine? |
|---|---|
| Dateien nach Endung in Ordner sortieren | `os`, `shutil`, Schleife, Bedingung |
| Logdatei nach Fehlern durchsuchen | Datei lesen, Bedingung, Zähler |
| CSV bereinigen oder zusammenfassen | `csv`, Schleife, Dictionary |
| Report aus Zahlen erstellen | Listen/Dicts, Funktionen, `print`/Datei |

---

## 9.2 Erst denken, dann tippen: Input → Verarbeitung → Output

```mermaid
flowchart LR
    A[Input<br/>Ordner / Datei / Eingabe] --> B[Verarbeitung<br/>Schritte definieren] --> C[Output<br/>neue Datei / Bildschirm]
```

Bevor du eine Zeile schreibst, beantworte drei Fragen:

1. **Input:** Was kommt rein? (Ein Ordner? Eine CSV? Eine Benutzereingabe?)
2. **Verarbeitung:** Welche Schritte sind nötig?
3. **Output:** Was soll am Ende dabei herauskommen?

---

## 9.3 Beispiel 1: Dateien nach Endung sortieren

Verschiebt alle Dateien aus einem Ordner in Unterordner nach ihrer Endung (`pdf/`, `jpg/`, …):

```python
import os
import shutil

quellordner = "downloads"
zielbasis = "sortiert"

for dateiname in os.listdir(quellordner):
    quellpfad = os.path.join(quellordner, dateiname)

    # Unterordner überspringen, nur Dateien bearbeiten
    if not os.path.isfile(quellpfad):
        continue

    # Endung bestimmen (z. B. ".pdf"), Punkt entfernen
    _, endung = os.path.splitext(dateiname)
    endung = endung.lower().strip(".") or "ohne_endung"

    zielordner = os.path.join(zielbasis, endung)
    os.makedirs(zielordner, exist_ok=True)   # Ordner anlegen, falls nicht da

    shutil.move(quellpfad, os.path.join(zielordner, dateiname))
    print(f"Verschoben: {dateiname} → {zielordner}")
```

!!! danger "Erst mit Kopien testen!"
    Dieses Skript **verschiebt echte Dateien**. Probiere es **niemals** zuerst an wichtigen Daten aus. Lege einen Test-Ordner mit ein paar Dummy-Dateien an und übe dort. Eine kaputte Automation kann viel Schaden anrichten – darum die wichtigste Regel: **erst testen, dann scharf schalten.**

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `os.listdir(ordner)` | `scandir($ordner)` / `glob()` |
    | `shutil.move(quelle, ziel)` | `rename($quelle, $ziel)` |
    | `os.makedirs(ordner, exist_ok=True)` | `mkdir($ordner, 0777, true)` |

    Wie in PHP: Automationen **immer zuerst mit Testdateien** probieren – echte Daten können sonst verschwinden.

---

## 9.4 Beispiel 2: Logdatei auswerten

Zählt, wie oft `ERROR` und `WARN` in einer Logdatei vorkommen:

```python
fehler = 0
warnungen = 0

with open("server.log", "r", encoding="utf-8") as log:
    for zeile in log:
        if "ERROR" in zeile:
            fehler += 1
        elif "WARN" in zeile:
            warnungen += 1

print(f"Fehler: {fehler}, Warnungen: {warnungen}")
```

`"ERROR" in zeile` prüft, ob der Text in der Zeile vorkommt – schlicht und wirkungsvoll. `fehler += 1` ist die Kurzform für `fehler = fehler + 1`.

---

## 9.5 Beispiel 3: Verkäufe aus einer CSV zusammenfassen

Hier kommt alles zusammen – Datei, CSV, Schleife, Bedingung, ein Dictionary als Sammler:

```python
import csv

gesamt = 0
pro_produkt = {}

with open("verkaeufe.csv", "r", encoding="utf-8") as datei:
    reader = csv.DictReader(datei)
    for row in reader:
        produkt = row["Produkt"]
        umsatz = float(row["Umsatz"])
        gesamt += umsatz
        pro_produkt[produkt] = pro_produkt.get(produkt, 0) + umsatz

print(f"Gesamtumsatz: {gesamt:.2f} €")
for name, summe in pro_produkt.items():
    print(f"  {name}: {summe:.2f} €")
```

!!! info "Zwei neue Kniffe"
    **`pro_produkt.get(produkt, 0)`** holt den bisherigen Wert oder `0`, falls das Produkt noch nicht vorkam – so musst du nicht prüfen, ob der Schlüssel schon existiert.
    **`{gesamt:.2f}`** formatiert die Zahl auf 2 Nachkommastellen (z. B. `19.50`).

??? info "Häufig gefragt: Was ist ein Dictionary?"
    Ein **Dictionary** (`{}`) speichert Paare aus **Schlüssel → Wert**, z. B. `{"Apfel": 3, "Birne": 5}`. Du greifst per Schlüssel zu: `preise["Apfel"]`. Ideal zum „Sammeln und Zusammenzählen" – genau das passiert hier mit `pro_produkt`.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `{"Apfel": 3}` | `["Apfel" => 3]` |
    | `preise["Apfel"]` | `$preise["Apfel"]` |
    | `preise.get("Apfel", 0)` | `$preise["Apfel"] ?? 0` |
    | `for k, v in d.items():` | `foreach ($d as $k => $v)` |

---

## 9.6 Checkliste vor dem ersten echten Einsatz

- [ ] Mit Testdaten / Kopien getestet?
- [ ] Pfade relativ und nachvollziehbar?
- [ ] Was passiert, wenn eine Datei fehlt? (Erwartung kennen)
- [ ] Gibt das Skript verständlich aus, **was** es getan hat?

!!! tip "Der wichtigste Satz dieses Kapitels"
    Eine Automation ist erst dann gut, wenn du ihr **vertrauen** kannst. Vertrauen entsteht durch **Testen mit harmlosen Daten** – nicht durch Hoffnung.

---

## Kurzübungen

{{ task(file="tasks/tag9_01.yaml") }}

{{ task(file="tasks/tag9_02.yaml") }}

{{ task(file="tasks/tag9_03.yaml") }}
