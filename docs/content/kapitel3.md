# Kapitel 3 – Strings & Text verarbeiten

<div class="kurs-progress">
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step active"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
</div>

<div class="lernziele" markdown>
<h3>Was du in diesem Kapitel lernst</h3>

- Texte (Strings) gezielt auslesen, kürzen und zusammensetzen
- Häufige String-Methoden wie `split()`, `strip()` und `replace()` nutzen
- Mit Slicing einzelne Teile eines Textes herausnehmen
- Texte für Ausgabe und einfache Datenaufbereitung formatieren
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Wiederholung & Anknüpfung</span>
**Das kennst du schon** aus dem ersten Kursteil: Strings in Anführungszeichen, `print()` und einfache f-Strings.

**Neu / hier wichtig:** Text **bearbeiten** statt nur ausgeben – genau das brauchst du später bei Logdateien, CSV-Zeilen und Automationen.
</div>

## So gehst du vor

1. Tippe jedes Beispiel ab und probiere kleine Variationen aus.
2. Achte darauf, ob eine Methode den **Original-Text verändert** oder einen **neuen** Text zurückgibt.
3. Bearbeite die **Kurzübungen**.

---

## 3.1 Was ist ein String?

Ein **String** (`str`) ist eine Zeichenkette – also Text. In Python steht er in `"..."` oder `'...'`.

```python
name = "Anna"
email = "anna@example.com"
```

Strings sind in der Praxis überall: Benutzereingaben, Dateiinhalte, CSV-Zeilen, Fehlermeldungen, Konfigurationen.

---

## 3.2 Länge und einzelne Zeichen

```python
text = "Python"
print(len(text))    # 6
print(text[0])      # P  (erstes Zeichen, Index 0)
print(text[-1])     # n  (letztes Zeichen)
```

Wie bei Listen beginnt der Index bei **0**. Negative Indizes zählen vom Ende.

---

## 3.3 Slicing – Teile herausschneiden

Mit **Slicing** nimmst du einen Ausschnitt aus einem Text:

```python
email = "anna@example.com"

print(email[0:4])    # anna
print(email[5:])     # example.com  (ab Index 5 bis Ende)
print(email[-3:])    # com
```

| Ausdruck | Bedeutung |
|---|---|
| `text[a:b]` | von Index `a` bis **vor** `b` |
| `text[a:]` | ab Index `a` bis Ende |
| `text[:b]` | vom Anfang bis **vor** `b` |

!!! tip "Praxis: Domain aus E-Mail extrahieren"
    `email.split("@")[1]` ist oft einfacher als Slicing – dazu gleich mehr.

---

## 3.4 String-Methoden – Text bearbeiten

Strings haben **Methoden** – Funktionen, die du mit einem Punkt am String aufrufst:

```python
text = "  Hallo Welt  "

print(text.strip())        # "Hallo Welt"  (Leerzeichen weg)
print(text.lower())        # "  hallo welt  "
print(text.upper())        # "  HALLO WELT  "
print(text.replace("Welt", "Python"))  # "  Hallo Python  "
```

Wichtig: Methoden wie `strip()` oder `lower()` erzeugen einen **neuen** String. Der Original-Text in `text` bleibt unverändert, solange du ihn nicht neu zuweist:

```python
text = text.strip()   # jetzt ist text bereinigt
```

### Text zerlegen und wieder zusammensetzen

```python
zeile = "Anna;2;Informatik"
teile = zeile.split(";")
print(teile)   # ['Anna', '2', 'Informatik']

print(teile[0])   # Anna
print(teile[1])   # 2

wieder = "-".join(teile)
print(wieder)   # Anna-2-Informatik
```

| Methode | Wofür? |
|---|---|
| `split("...")` | Text an einem Trennzeichen **zerlegen** → Liste |
| `join(liste)` | Liste-Elemente mit Trennzeichen **verbinden** → String |

!!! info "IT-Bezug"
    Eine CSV-Zeile wie `Anna,2,Informatik` ist im Kern ein String mit Trennzeichen. Später nutzt du dafür das `csv`-Modul (Kapitel 8) – das Prinzip ist aber dasselbe.

---

## 3.5 Prüfen, ob Text vorkommt

```python
log = "2026-06-22 ERROR: Verbindung fehlgeschlagen"

if "ERROR" in log:
    print("Fehler gefunden!")
```

`in` prüft, ob ein Teilstring vorkommt – sehr nützlich bei Logdateien und einfachen Filtern.

---

## 3.6 Text schön formatieren

f-Strings kannst du **formatieren**:

```python
preis = 19.5
menge = 3
print(f"Summe: {preis * menge:.2f} €")   # Summe: 58.50 €
```

`:.2f` bedeutet: Kommazahl mit **2 Nachkommastellen**.

Weitere nützliche Varianten:

```python
name = "anna"
print(f"Hallo, {name.title()}!")   # Hallo, Anna!
print(f"{'Produkt':<12} {'Preis':>8}")
print(f"{'Apfel':<12} {1.20:>8.2f}")
```

---

## 3.7 Kleines Beispiel: Eingabe bereinigen

```python
raw = input("E-Mail eingeben: ")
email = raw.strip().lower()

if "@" not in email:
    print("Das sieht nicht wie eine E-Mail aus.")
else:
    print(f"Gespeichert: {email}")
```

Hier kombinierst du **Methoden-Kette** (`strip().lower()`) mit einer **Prüfung** (`in` / `not in`).

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `text.strip()` | `trim($text)` |
    | `text.lower()` | `strtolower($text)` |
    | `text.split(";")` | `explode(";", $text)` |
    | `"-".join(liste)` | `implode("-", $liste)` |

    In Python steht der String **vor** dem Punkt: `email.strip()`, nicht `$email->strip()`.

---

## Kurzübungen

{{ task(file="tasks/tag3_01.yaml") }}

{{ task(file="tasks/tag3_02.yaml") }}

{{ task(file="tasks/tag3_03.yaml") }}
