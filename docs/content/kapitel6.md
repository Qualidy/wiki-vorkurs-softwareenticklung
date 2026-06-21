# Kapitel 6 – Schleifen & Listen

<div class="kurs-progress">
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step active"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
  <div class="step"></div>
</div>

<div class="lernziele" markdown>
<h3>Was du in diesem Kapitel lernst</h3>

- Wiederholungen mit `for` und `while` umsetzen
- `range()` für Zählschleifen nutzen
- Listen anlegen, durchlaufen und verändern
- Einfache Auswertungen (Summe, Maximum) selbst programmieren
- `break` und `continue` gezielt einsetzen
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Wiederholung & Anknüpfung</span>
**Das kennst du schon** aus dem ersten Kursteil: die `for`- und `while`-Schleife, `range()`, Listen sowie `append()`, `remove()`, `len()` und den Zugriff per Index.

**Neu / hier wichtig:** Wir schärfen die Frage „**wann `for`, wann `while`?**", zeigen den häufigsten Schleifen-Fehler (Endlosschleife) und üben kleine Auswertungen **ohne** fertige Funktionen wie `sum()`/`max()` – damit das Prinzip sitzt.
</div>

## So gehst du vor

1. Frag dich vor jeder Schleife: **Wie oft** soll wiederholt werden – feste Anzahl (`for`) oder bis eine Bedingung kippt (`while`)?
2. Übe den Listen-Index: das **erste** Element hat Index **0**.
3. Bearbeite die **Kurzübungen** – viele bewusst ohne `min()`, `max()`, `sum()`.

---

## 6.1 for-Schleife mit `range()`

Eine `for`-Schleife wiederholt etwas **eine feste Anzahl** Mal.

```python
for i in range(5):
    print(i)
```

**Ausgabe:**

```
0
1
2
3
4
```

| Ausdruck | Erzeugt |
|---|---|
| `range(5)` | 0, 1, 2, 3, 4 |
| `range(2, 8)` | 2, 3, 4, 5, 6, 7 |
| `range(0, 10, 2)` | 0, 2, 4, 6, 8 |

!!! warning "Stolperstein: `range(5)` hört bei 4 auf"
    `range(5)` erzeugt **fünf** Zahlen, aber **0 bis 4** – nicht bis 5. Die Obergrenze ist immer **ausgeschlossen**. Das ist der berühmte „off-by-one"-Fehler.

---

## 6.2 while-Schleife

Eine `while`-Schleife läuft, **solange eine Bedingung wahr ist**.

```python
zahl = 0
while zahl < 5:
    print(zahl)
    zahl = zahl + 1
```

Drei Dinge gehören dazu:

1. Die Variable **vorher** setzen (`zahl = 0`)
2. Die **Bedingung** (`zahl < 5`)
3. Die Variable **in der Schleife verändern** (`zahl = zahl + 1`)

!!! warning "Stolperstein: die Endlosschleife"
    Vergisst du den Schritt `zahl = zahl + 1`, bleibt die Bedingung für immer wahr – das Programm läuft endlos und gibt unaufhörlich `0` aus. **Abbrechen** kannst du im Terminal mit ++ctrl+c++.

??? info "Häufig gefragt: Wann nehme ich `for`, wann `while`?"
    Faustregel: **`for`**, wenn du die Anzahl der Durchläufe kennst oder eine Liste/Range durchgehst. **`while`**, wenn du nicht weißt, wie oft – z. B. „so lange, bis der Benutzer `stop` eingibt". Im Zweifel ist `for` die sicherere Wahl (keine Endlosschleifen-Gefahr).

---

## 6.3 Listen – mehrere Werte in einer Variablen

```python
zahlen = [1, 2, 3, 4, 5]
namen = ["Anna", "Bob", "Charlie"]
```

| Was | Code | Ergebnis |
|---|---|---|
| Erstes Element | `zahlen[0]` | `1` |
| Drittes Element | `zahlen[2]` | `3` |
| Letztes Element | `zahlen[-1]` | `5` |
| Anzahl | `len(zahlen)` | `5` |
| Anhängen | `zahlen.append(6)` | Liste wird `[1,2,3,4,5,6]` |
| Entfernen | `zahlen.remove(3)` | Liste wird `[1,2,4,5,6]` |

!!! warning "Stolperstein: Index beginnt bei 0"
    Bei `["Anna", "Bob", "Charlie"]` ist `[0]` = Anna, `[1]` = Bob, `[2]` = Charlie. Greifst du auf `[3]` zu, kommt:

    ```
    IndexError: list index out of range
    ```

    → Das letzte Element erreichst du sicher mit `[-1]`.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `zahlen = [1, 2, 3]` | `$zahlen = [1, 2, 3];` |
    | `zahlen[0]` | `$zahlen[0]` |
    | `zahlen.append(6)` | `$zahlen[] = 6;` |
    | `len(zahlen)` | `count($zahlen)` |

    Python-Listen sind flexibler als klassische PHP-Arrays – für den Anfang reicht die Analogie.

---

## 6.4 Über eine Liste iterieren

Statt mit Indizes kannst du direkt **durch die Elemente** gehen:

```python
noten = [2, 3, 1, 4, 2]

for note in noten:
    print(note)
```

Bei jedem Durchlauf nimmt `note` automatisch das nächste Element an. Sauberer und lesbarer als der Umweg über `range(len(...))`.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    ```python
    for note in noten:
        print(note)
    ```

    entspricht ungefähr:

    ```php
    foreach ($noten as $note) {
        echo $note;
    }
    ```

    `for i in range(5):` ist eher vergleichbar mit `for ($i = 0; $i < 5; $i++)`.

---

## 6.5 Beispiel: Summe berechnen (ohne `sum()`)

```python
zahlen = [4, 8, 1, 9, 3]
summe = 0

for zahl in zahlen:
    summe = summe + zahl

print(f"Summe: {summe}")   # Summe: 25
```

Das Muster „**Sammelvariable vor der Schleife, in der Schleife erhöhen**" brauchst du ständig.

---

## 6.6 Beispiel: Größte Zahl finden (ohne `max()`)

```python
zahlen = [4, 8, 1, 9, 3]
groesste = zahlen[0]

for zahl in zahlen:
    if zahl > groesste:
        groesste = zahl

print(f"Größte Zahl: {groesste}")   # Größte Zahl: 9
```

Hier kombinierst du Schleife **und** Bedingung – genau das übst du in den Aufgaben.

---

## 6.7 break und continue

| Befehl | Wirkung |
|---|---|
| `break` | Schleife **sofort** komplett beenden |
| `continue` | Aktuellen Durchlauf **überspringen**, mit dem nächsten weitermachen |

```python
for zahl in [1, 2, 3, 4, 5, 6]:
    if zahl == 4:
        break          # bei 4 ist Schluss
    print(zahl)        # gibt 1, 2, 3 aus
```

---

## Kurzübungen

{{ task(file="tasks/tag6_01.yaml") }}

{{ task(file="tasks/tag6_02.yaml") }}

{{ task(file="tasks/tag6_03.yaml") }}
