# Kapitel 4 – Datentypen, Variablen & Ein-/Ausgabe

<div class="kurs-progress">
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step active"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
</div>

<div class="lernziele" markdown>
<h3>Was du in diesem Kapitel lernst</h3>

- Variablen anlegen und Werte darin speichern
- Die wichtigsten Datentypen: `str`, `int`, `float`, `bool`
- Text und Zahlen sauber ausgeben – besonders mit f-Strings
- Eingaben mit `input()` einlesen und in Zahlen umwandeln
- Mit den Grundrechenarten in Python rechnen
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Wiederholung & Anknüpfung</span>
**Das kennst du schon** aus dem ersten Kursteil: Variablen, die Datentypen `str`/`int`/`float`, die `print()`-Varianten und Eingaben mit `input()`.

**Neu / hier wichtig:** Wir frischen das kompakt auf und schauen gezielt auf die typischen **Stolpersteine** (Text + Zahl mischen, `input()` ist immer Text, Komma vs. Punkt) – genau die Fragen, die im Kurs erfahrungsgemäß kommen.
</div>

## So gehst du vor

1. Tippe **jedes** Beispiel selbst ab und führe es aus – nur Lesen reicht nicht.
2. Experimentiere bewusst: Was passiert, wenn du Text und Zahl mischst?
3. Bearbeite die **Kurzübungen** von einfach bis anspruchsvoller.

---

## 4.1 Was ist eine Variable?

Eine **Variable** ist ein **benannter Behälter** für einen Wert. Du gibst dem Wert einen Namen und kannst ihn später immer wieder benutzen, statt ihn erneut einzutippen.

```python
name = "Anna"
alter = 25
preis = 19.99
```

| Bestandteil | Beispiel | Erklärung |
|---|---|---|
| Variablenname | `name` | Frei wählbar (sprechend benennen!) |
| Zuweisungsoperator | `=` | „bekommt den Wert von" |
| Wert | `"Anna"` | Das, was gespeichert wird |

Man liest `name = "Anna"` als: **„name bekommt den Wert Anna"** – *nicht* als „ist gleich".

!!! warning "Stolperstein: Groß-/Kleinschreibung zählt"
    `Name` und `name` sind für Python **zwei verschiedene** Variablen. Wer `name = "Anna"` schreibt und später `print(Name)` aufruft, bekommt einen `NameError`.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `name = "Anna"` | `$name = "Anna";` |
    | dynamische Typen | ebenfalls dynamisch (`$x = 5; $x = "hi";`) |
    | `True` / `False` | `true` / `false` |

    Python nutzt **kein** `$` vor Variablennamen und **kein** Semikolon am Zeilenende.

---

## 4.2 Die wichtigsten Datentypen

| Typ | Python-Name | Beispiel | Was es ist |
|---|---|---|---|
| Text | `str` | `"Hallo"` | Zeichenkette (String) |
| Ganzzahl | `int` | `42` | Zahl ohne Komma |
| Kommazahl | `float` | `3.14` | Zahl mit Komma (Punkt!) |
| Wahrheitswert | `bool` | `True`, `False` | wahr oder falsch |

Den Typ eines Werts prüfst du mit `type()`:

```python
print(type("Hallo"))   # <class 'str'>
print(type(42))        # <class 'int'>
print(type(3.14))      # <class 'float'>
```

!!! warning "Stolperstein: Kommazahlen mit Punkt"
    Python schreibt Kommazahlen mit **Punkt**, nicht mit Komma: `3.14`, nicht `3,14`. Ein Komma würde Python als zwei getrennte Werte verstehen.

---

## 4.3 Ausgabe mit `print()`

### Variante 1: f-String (empfohlen)

Setze ein **`f`** direkt vor das Anführungszeichen. Dann kannst du Variablen in geschweiften Klammern `{}` mitten in den Text schreiben:

```python
name = "Anna"
alter = 25
print(f"Ich heiße {name} und bin {alter} Jahre alt.")
```

**Ausgabe:**

```
Ich heiße Anna und bin 25 Jahre alt.
```

### Variante 2: Verketten mit `+`

```python
print("Ich heiße " + name + " und bin " + str(alter) + " Jahre alt.")
```

Hier ist `str(alter)` nötig: Mit `+` kann man nur **Text mit Text** verbinden – die Zahl muss erst in Text umgewandelt werden.

### Variante 3: mit Komma trennen

```python
print("Ich heiße", name, "und bin", alter, "Jahre alt")
```

Hier setzt Python automatisch Leerzeichen zwischen die Teile.

!!! tip "Empfehlung"
    Nimm im Zweifel den **f-String** (Variante 1). Er ist am besten lesbar und du musst Zahlen nicht extra umwandeln.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `f"Hallo {name}"` | `"Hallo $name"` oder `"Hallo {$name}"` |
    | `"Text " + str(42)` | `"Text " . 42` (PHP castet automatisch) |

    In Python musst du beim `+`-Verketten Zahlen explizit mit `str()` umwandeln – deshalb sind f-Strings bequemer.

!!! warning "Häufiger Fehler: Text und Zahl mit `+` mischen"
    `print("Alter: " + 25)` führt zu:

    ```
    TypeError: can only concatenate str (not "int") to str
    ```

    → Entweder `str(25)` verwenden oder – einfacher – einen f-String: `print(f"Alter: {25}")`.

---

## 4.4 Eingabe mit `input()`

`input()` liest eine Eingabe von der Tastatur. **Wichtig:** Das Ergebnis ist **immer ein Text (`str`)** – auch wenn der Benutzer eine Zahl eintippt.

```python
name = input("Wie heißt du? ")
print(f"Hallo, {name}!")
```

### Zahlen einlesen

Damit du mit einer Eingabe rechnen kannst, musst du sie umwandeln:

```python
alter = int(input("Wie alt bist du? "))
groesse = float(input("Wie groß bist du (in m)? "))
```

| Funktion | Wandelt um in | Beispiel |
|---|---|---|
| `int(...)` | Ganzzahl | `"25"` → `25` |
| `float(...)` | Kommazahl | `"1.80"` → `1.8` |
| `str(...)` | Text | `25` → `"25"` |

!!! warning "Häufiger Fehler: ungültige Zahl bei `int()`"
    Gibt der Benutzer Buchstaben oder ein Komma ein (`1,80` statt `1.80`), kommt:

    ```
    ValueError: invalid literal for int() with base 10: 'abc'
    ```

    → Das ist erwartbar. Wie man solche Fälle abfängt, lernst du später; im Vorkurs reicht es, den Fehler zu **erkennen** und zu wissen, woher er kommt.

??? info "Häufig gefragt: Warum ist `input()` immer Text – auch bei Zahlen?"
    Weil Python beim Einlesen nicht weiß, ob du eine Zahl, einen Namen oder ein Datum meinst. Es nimmt erstmal alles als Text. **Du** entscheidest mit `int()` oder `float()`, dass daraus eine Zahl werden soll.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    `input()` liest von der **Konsole** (Terminal) – vergleichbar mit `trim(fgets(STDIN))` in einem CLI-Skript.

    Das ist **nicht** dasselbe wie `$_GET` / `$_POST` im Browser – die kommen erst bei Web-Programmierung vor. Zahlen casten: `int(input(...))` entspricht ungefähr `(int) $_GET['alter']`.

---

## 4.5 Ein kleines Gesprächsprogramm

```python
name = input("Wie heißt du? ")
alter = int(input("Wie alt bist du? "))
print(f"Schön, {name} — mit {alter} Jahren hast du noch viel vor!")
```

Drei Zeilen, ein vollständiges interaktives Programm. Genau solche kleinen Bausteine kombinieren wir in den nächsten Kapiteln zu größeren Programmen.

---

## 4.6 Rechnen in Python

| Operator | Bedeutung | Beispiel | Ergebnis |
|---|---|---|---|
| `+` | Addition | `3 + 2` | `5` |
| `-` | Subtraktion | `5 - 2` | `3` |
| `*` | Multiplikation | `4 * 3` | `12` |
| `/` | Division | `7 / 2` | `3.5` |
| `//` | Ganzzahldivision (rundet ab) | `7 // 2` | `3` |
| `%` | Modulo (Rest) | `7 % 2` | `1` |
| `**` | Potenz | `2 ** 3` | `8` |

!!! tip "Modulo ist praktischer als es klingt"
    `%` gibt den **Rest** einer Division zurück. Damit prüfst du z. B. ganz einfach, ob eine Zahl gerade ist: `zahl % 2 == 0` ist genau dann wahr, wenn `zahl` gerade ist. Das brauchst du in den Übungen immer wieder.

---

## Kurzübungen

{{ task(file="tasks/tag4_01.yaml") }}

{{ task(file="tasks/tag4_02.yaml") }}

{{ task(file="tasks/tag4_03.yaml") }}
