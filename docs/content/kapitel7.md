# Kapitel 7 – Funktionen & Module

<div class="kurs-progress">
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step active"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
</div>

<div class="lernziele" markdown>
<h3>Was du in diesem Kapitel lernst</h3>

- Funktionen mit `def` definieren, aufrufen und Werte zurückgeben (Auffrischung)
- Parameter, Rückgabewerte und Default-Argumente sicher nutzen
- **Neu:** Code in **Module** auslagern und mit `import` wiederverwenden
- **Neu:** das Import-Prinzip verstehen (`import`, `from … import …`, Alias)
- Die Standardbibliothek nutzen (`math`, `random`, …)
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Wiederholung & Anknüpfung</span>
**Das kennst du schon** aus dem ersten Kursteil: Funktionen mit `def`, Parameter, `return`, Default-/`*args`-Argumente und Rekursion.

**Neu / Schwerpunkt dieses Kapitels:** das **Modul- und Import-Prinzip**. Funktionen frischen wir nur kurz auf – die eigentliche neue Fähigkeit ist, Code in **eigene Dateien (Module)** auszulagern und fertige Bausteine mit `import` zu nutzen.
</div>

## So gehst du vor

1. Überflieg die Auffrischung zu Funktionen (Abschnitt 7.1–7.4).
2. Nimm dir **Zeit für 7.6–7.8** – Module und `import` sind hier das neue Thema.
3. Bearbeite die **Kurzübungen**.

---

## 7.1 Funktionen – kurze Auffrischung

Eine **Funktion** ist ein **wiederverwendbarer Code-Block**: einmal schreiben, beliebig oft aufrufen.

```python
def greet():
    print("Hallo!")

greet()
greet()   # beliebig oft aufrufbar
```

---

## 7.2 Parameter und Rückgabewerte

```python
def add(a, b):
    return a + b

ergebnis = add(5, 3)
print(ergebnis)   # 8
```

- **Parameter** (`a`, `b`) sind Platzhalter, die beim Aufruf mit Werten gefüllt werden.
- **`return`** gibt ein Ergebnis zurück, mit dem du weiterarbeiten kannst.

!!! warning "Stolperstein: `return` ist nicht `print`"
    `print()` **zeigt** etwas am Bildschirm, `return` **gibt einen Wert zurück**, mit dem das Programm weiterrechnen kann. Eine Funktion, die nur `print()` macht, liefert als Rückgabe `None`. Wer mit dem Ergebnis weiterrechnen will, braucht `return`.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `def add(a, b):` | `function add($a, $b) {` |
    | `return a + b` | `return $a + $b;` |
    | `def greet(name="Anna"):` | `function greet($name = "Anna") {` |

    `return` funktioniert in beiden Sprachen gleich. In PHP darfst du nicht vergessen, Funktionsaufrufe mit `$` zu schreiben: `$ergebnis = add(5, 3);`.

---

## 7.3 Default-Parameter

Parameter können einen **Standardwert** haben, der greift, wenn beim Aufruf nichts übergeben wird:

```python
def begruesse(name, sprache="Deutsch"):
    if sprache == "Deutsch":
        print(f"Hallo, {name}!")
    elif sprache == "Englisch":
        print(f"Hello, {name}!")
    else:
        print(f"Bonjour, {name}!")

begruesse("Anna")              # Hallo, Anna!
begruesse("Anna", "Englisch")  # Hello, Anna!
```

---

## 7.4 Docstrings – kurz dokumentieren

```python
def bmi(gewicht, groesse):
    """Berechnet den Body-Mass-Index."""
    return gewicht / (groesse ** 2)
```

Der Text in `"""..."""` direkt unter `def` beschreibt, was die Funktion tut. Gute Gewohnheit – und VS Code zeigt ihn später als Hilfe an.

---

## 7.5 Warum Funktionen ausklammern? → Module

Bisher stand aller Code in **einer** Datei. Sobald ein Projekt wächst, wird das unübersichtlich. Die Lösung: zusammengehörige Funktionen in **eigene Dateien** legen – solche Dateien heißen in Python **Module**.

Ein **Modul ist einfach eine `.py`-Datei.** Mehr nicht.

---

## 7.6 Eigenes Modul erstellen und importieren

**Datei `werkzeuge.py`** (das Modul):

```python
def quadrat(zahl):
    return zahl * zahl

def begruessung(name):
    return f"Hallo, {name}!"
```

**Datei `main.py`** (nutzt das Modul):

```python
import werkzeuge

print(werkzeuge.quadrat(5))        # 25
print(werkzeuge.begruessung("Tom")) # Hallo, Tom!
```

Wichtig: Beim `import` schreibst du den **Dateinamen ohne `.py`** – also `import werkzeuge`, nicht `import werkzeuge.py`. Danach erreichst du die Funktionen über `modulname.funktion(...)`.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `import werkzeuge` | `require 'werkzeuge.php';` |
    | `werkzeuge.quadrat(5)` | nach `require` meist direkt `quadrat(5)` |
    | `from math import sqrt` | einzelne Funktion per `require` + direkter Aufruf |

    Der große Unterschied: Python-Module bleiben **eindeutig benannt** (`modul.funktion`) – weniger Namenskonflikte als bei globalem `require`.

---

## 7.7 Die drei Import-Varianten

| Schreibweise | Aufruf danach | Wann sinnvoll |
|---|---|---|
| `import math` | `math.sqrt(16)` | Standard – Herkunft bleibt sichtbar |
| `from math import sqrt` | `sqrt(16)` | Wenn du nur **eine** Funktion oft brauchst |
| `import datetime as dt` | `dt.datetime.now()` | Langer Modulname → kurzer Alias |

```python
import math
print(math.sqrt(144))      # 12.0

from random import randint
print(randint(1, 6))       # eine Zufallszahl von 1 bis 6
```

!!! info "Eingebaute Module: die Standardbibliothek"
    Python bringt **hunderte** fertige Module mit, ohne Installation. Die wichtigsten für den Anfang:

    | Modul | Wofür |
    |---|---|
    | `math` | Wurzel, Runden, Pi … |
    | `random` | Zufallszahlen |
    | `datetime` | Datum und Uhrzeit |
    | `os` | Dateien/Ordner (Kapitel 9) |
    | `csv`, `json` | Datenformate (Kapitel 8) |

---

## 7.8 Externe Pakete mit `pip`

Reicht die Standardbibliothek nicht, holst du dir **externe Pakete** mit `pip` (siehe Kapitel 2) – z. B. `requests` für Web-Zugriffe. Nach der Installation funktioniert das `import` genauso:

```python
import requests   # vorher: pip install requests
```

!!! warning "Häufige Fehler beim Import"
    **`ModuleNotFoundError: No module named 'werkzeug'`**

    → Tippfehler im Namen, **oder** die Modul-Datei liegt nicht im selben Ordner, **oder** ein externes Paket wurde nicht mit `pip install` installiert (bzw. die falsche `venv` ist aktiv).

    **`ModuleNotFoundError: No module named 'werkzeuge.py'`**

    → Du hast `.py` mitgeschrieben. Richtig: `import werkzeuge` (ohne Endung).

---

## 7.9 Rekursion – Kurzüberblick

Zur Erinnerung: Eine Funktion, die **sich selbst** aufruft. Sie braucht einen **Basis-Fall** (Stopp) und einen **rekursiven Fall**.

```python
def countdown(n):
    if n == 0:
        print("Fertig!")
        return
    print(n)
    countdown(n - 1)

countdown(4)   # 4, 3, 2, 1, Fertig!
```

!!! tip "Im Vorkurs reicht das Prinzip"
    Rekursion ist mächtig, für Einsteiger aber oft schwerer zu durchschauen als eine Schleife. Verstehe das Grundprinzip – Fakultät, Palindrome & Co. sind Vertiefung, kein Pflichtstoff.

---

## Kurzübungen

{{ task(file="tasks/tag7_01.yaml") }}

{{ task(file="tasks/tag7_02.yaml") }}

{{ task(file="tasks/tag7_03.yaml") }}
