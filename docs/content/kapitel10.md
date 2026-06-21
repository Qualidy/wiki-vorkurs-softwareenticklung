# Kapitel 10 – Dictionaries & Datenstrukturen

<div class="kurs-progress">
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step done"></div>
  <div class="step active"></div>
</div>

<div class="lernziele" markdown>
<h3>Was du in diesem Kapitel lernst</h3>

- Mit **Dictionaries** Daten als Schlüssel-Wert-Paare speichern
- Werte abfragen, ändern und sicher auslesen mit `.get()`
- Über Dictionaries iterieren – Vorbereitung für Auswertungen und Automationen
- Kurzüberblick: **Sets** und **Tuples**
- Den Vorkurs einordnen: Was du jetzt kannst und was als Nächstes kommt
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Wiederholung & Anknüpfung</span>
**Das kennst du schon:** Listen (Kapitel 6), CSV-Zeilen als Dictionary beim Einlesen (Kapitel 8) und das Sammeln von Werten in Automationen (Kapitel 9).

**Neu / hier wichtig:** Dictionaries **bewusst** verstehen und selbst bauen – damit Code wie `produkte.get(name, 0)` und JSON-Daten keine Black Box mehr sind.
</div>

## So gehst du vor

1. Vergleiche Dictionary-Zugriff mit Listen-Index – beides ist Alltag in Python.
2. Nutze `.get()` statt direktem `[...]`-Zugriff, wenn ein Schlüssel fehlen könnte.
3. Bearbeite die **Kurzübungen** zum Abschluss des Vorkurses.

---

## 10.1 Was ist ein Dictionary?

Ein **Dictionary** (`dict`) speichert **Schlüssel → Wert** – wie ein Wörterbuch oder eine Konfigurationstabelle:

```python
server = {
    "name": "web-01",
    "cpu": 45,
    "online": True
}

print(server["name"])    # web-01
print(server["cpu"])     # 45
```

| Listen | Dictionaries |
|---|---|
| Zugriff per **Zahl** (Index): `[0]` | Zugriff per **Schlüssel**: `["name"]` |
| Geordnete Reihenfolge | Schlüssel sind eindeutig |
| Gut für gleichartige Werte | Gut für benannte Eigenschaften |

---

## 10.2 Werte ändern und hinzufügen

```python
server = {"name": "web-01", "cpu": 45}

server["cpu"] = 52          # Wert ändern
server["ram"] = 78          # neuen Schlüssel anlegen

print(server)   # {'name': 'web-01', 'cpu': 52, 'ram': 78}
```

Existiert der Schlüssel noch nicht, legt Python ihn an. Existiert er schon, wird der Wert überschrieben.

---

## 10.3 Sicher lesen mit `.get()`

```python
server = {"name": "web-01", "cpu": 45}

print(server.get("cpu"))           # 45
print(server.get("ram"))           # None  (Schlüssel fehlt)
print(server.get("ram", 0))        # 0     (Standardwert)
```

!!! warning "Stolperstein: KeyError"
    `server["ram"]` wirft einen Fehler, wenn `ram` nicht existiert:

    ```
    KeyError: 'ram'
    ```

    → Nutze `.get("ram", 0)`, wenn der Schlüssel optional ist – genau so in den Automationen aus Kapitel 9.

---

## 10.4 Über ein Dictionary iterieren

```python
umsatz = {"Apfel": 12.50, "Birne": 8.00, "Kiwi": 15.75}

for produkt in umsatz:
    print(produkt, umsatz[produkt])

for produkt, betrag in umsatz.items():
    print(f"{produkt}: {betrag:.2f} €")
```

| Schleife | Liefert |
|---|---|
| `for key in dict` | nur die Schlüssel |
| `for key, value in dict.items()` | Schlüssel **und** Wert |

Das Muster `dict[key] = dict.get(key, 0) + wert` aus Kapitel 9 ist damit klar: **Summieren nach Schlüssel**.

---

## 10.5 Dictionary aus CSV-Zeilen – Bezug zur Praxis

Eine CSV-Zeile als Dictionary (wie in Kapitel 8):

```python
row = {"Name": "Anna", "Note": "2", "Fach": "Informatik"}

print(f"{row['Name']} hat Note {row['Note']} in {row['Fach']}")
```

JSON ist strukturell dasselbe – nur in einer Datei gespeichert (Kapitel 8).

---

## 10.6 Sets und Tuples – Kurzüberblick

### Tuple – unveränderliche Liste

```python
koordinaten = (10, 20)
print(koordinaten[0])   # 10
```

Tuples eignen sich für feste Wertepaare, die sich nicht ändern sollen.

### Set – eindeutige Werte ohne Duplikate

```python
tags = {"python", "kurs", "python", "it"}
print(tags)   # {'python', 'kurs', 'it'}  – Duplikat weg
```

Sets sind praktisch, um **doppelte Einträge** zu entfernen oder schnell „schon gesehen?" zu prüfen.

!!! tip "Im Vorkurs reicht das Prinzip"
    Listen und Dictionaries sind die wichtigsten Strukturen. Sets und Tuples solltest du **kennen**, musst du aber am Anfang selten selbst einsetzen.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `server = {"name": "db-01"}` | `$server = ["name" => "db-01"];` |
    | `server["cpu"]` | `$server["cpu"]` |
    | `server.get("ram", 0)` | `$server["ram"] ?? 0` |
    | `for k, v in server.items():` | `foreach ($server as $k => $v)` |

---

## 10.7 Was du nach dem Vorkurs mitnehmen kannst

Du hast in fünf Tagen die **Grundlagen von Python** kennengelernt:

| Bereich | Beispiele |
|---|---|
| Sprache | Variablen, `if`, Schleifen, Funktionen |
| Struktur | Module, `import`, eigene `.py`-Dateien |
| Daten | Dateien, CSV, JSON, Dictionaries |
| Praxis | Kleine Skripte, die dir Arbeit abnehmen |

Typische nächste Schritte im Hauptkurs:

- größere Programme mit klarer Projektstruktur
- Fehlerbehandlung mit `try`/`except`
- Arbeit mit APIs und Bibliotheken
- objektorientierte Programmierung (Klassen)

!!! tip "Weiter üben"
    Die besten Übungen sind **eigene Mini-Probleme** aus deinem Alltag: Dateien sortieren, Texte bereinigen, kleine Listen auswerten. Je öfter du tippst, desto sicherer wirst du – Fehlermeldungen sind dabei normal und gehören dazu.

---

## Kurzübungen

{{ task(file="tasks/tag10_01.yaml") }}

{{ task(file="tasks/tag10_02.yaml") }}

{{ task(file="tasks/tag10_03.yaml") }}
