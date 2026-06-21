# Kapitel 2 – Python-Setup & Arbeitsumgebung

<div class="kurs-progress">
  <div class="step done"></div>
  <div class="step active"></div>
  <div class="step"></div>
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

- Welche zwei Programme du zum Python-Programmieren brauchst
- Python installieren und die Version im Terminal prüfen
- VS Code als Editor einrichten und die Python-Extension installieren
- Was eine virtuelle Umgebung (`venv`) ist und wie du Pakete mit `pip` installierst
- Dein erstes eigenes Programm schreiben und ausführen
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Wiederholung & Anknüpfung</span>
**Das kennst du schon** aus dem ersten Kursteil: VS Code, virtuelle Umgebungen (`venv`), `pip` und dein erstes „Hello World".

**Neu / hier wichtig:** Dieses Kapitel ist dein Nachschlagewerk fürs Setup – mit den häufigsten Fehlern und Lösungen, falls bei jemandem im Kurs die Umgebung klemmt.
</div>

## So gehst du vor

1. Folge der Anleitung **Schritt für Schritt am eigenen Laptop** mit.
2. Prüfe nach jedem Schritt, ob die erwartete Ausgabe erscheint.
3. Wenn etwas nicht klappt: schau in die Box **„Häufige Fehler"** weiter unten.
4. Bearbeite zum Schluss die **Kurzübungen**.

---

## 2.1 Was brauchst du überhaupt?

Zum Programmieren brauchst du **zwei** Dinge:

| Komponente | Aufgabe | Vergleich |
|---|---|---|
| **Python-Interpreter** | Führt deinen Code aus | Der „Motor" |
| **Editor / IDE** | Hier schreibst und speicherst du den Code (`.py`-Dateien) | Der „Schreibtisch" |

Gängige Editoren:

| Tool | Beschreibung |
|---|---|
| **VS Code** | Kostenlos, sehr verbreitet, starke Python-Unterstützung – **unsere Empfehlung im Kurs** |
| **PyCharm** | Vollwertige Python-IDE mit vielen Funktionen, etwas schwergewichtiger |
| **Trinket.io / Python Playground** | Läuft direkt im Browser, keine Installation – guter Notfall-Plan B |

!!! info "Interpreter, Editor, IDE – was ist der Unterschied?"
    Der **Interpreter** ist das eigentliche Python-Programm, das Code ausführt. Ein **Editor** ist ein Schreibprogramm für Code. Eine **IDE** (Integrated Development Environment) ist ein Editor mit Extras wie Fehleranzeige und Debugger. VS Code wird durch die Python-Extension zu einer kleinen IDE.

---

## 2.2 Python installieren und Version prüfen

### Schritt 1: Terminal öffnen

Das **Terminal** ist ein Fenster, in das du Befehle eintippst (kein Klick-Menü). In VS Code öffnest du es über **Terminal → New Terminal**.

### Schritt 2: Prüfen, ob Python schon da ist

Tippe im Terminal:

```bash
python --version
```

Auf manchen Systemen (besonders macOS/Linux) heißt der Befehl:

```bash
python3 --version
```

**Erwartete Ausgabe** (Zahl kann abweichen):

```
Python 3.12.3
```

Erscheint eine Versionsnummer, ist Python installiert – weiter mit 2.3.

### Schritt 3: Python installieren (nur falls nötig)

Wenn stattdessen eine Fehlermeldung kommt, lade Python von [python.org/downloads](https://www.python.org/downloads/) und installiere es.

!!! warning "Windows: Häkchen bei „Add Python to PATH" setzen"
    Im Windows-Installer **unbedingt** unten das Kästchen **„Add python.exe to PATH"** anhaken, **bevor** du auf „Install Now" klickst. Ohne dieses Häkchen findet das Terminal den Befehl `python` später nicht – der mit Abstand häufigste Stolperstein bei der Installation.

??? warning "Häufige Fehler bei der Installation"
    **`python : The term 'python' is not recognized ...` (Windows)** oder **`command not found: python` (macOS/Linux)**

    → Python ist nicht installiert **oder** nicht im PATH. Unter Windows: Python neu installieren und das PATH-Häkchen setzen. Unter macOS/Linux: stattdessen `python3` probieren.

    **`python` öffnet den Microsoft Store (Windows 11)**

    → Das ist ein Windows-Platzhalter. Installiere Python von python.org oder probiere `python3`.

---

## 2.3 VS Code für Python vorbereiten

Die offizielle **Python-Extension** macht VS Code „Python-schlau":

1. Linke Seitenleiste: auf das **Extensions-Symbol** (vier Quadrate) klicken
2. Im Suchfeld **„Python"** eingeben
3. Die offizielle Extension von **Microsoft** auswählen und **Install** klicken

Was die Extension mitbringt:

| Funktion | Nutzen |
|---|---|
| Syntax-Highlighting | Code wird farbig – Fehler fallen schneller auf |
| Code-Vorschläge | Vorschläge beim Tippen (Autovervollständigung) |
| Fehleranzeige | Offensichtliche Fehler werden rot unterkringelt |
| Debugger | Code Schritt für Schritt durchlaufen, Variablen beobachten |

---

## 2.4 Virtuelle Umgebungen (`venv`)

Eine **virtuelle Umgebung** ist ein **isolierter Ordner** für die Zusatzpakete *eines* Projekts. So vermischen sich die Pakete verschiedener Projekte nicht.

!!! info "Warum überhaupt isolieren?"
    Projekt A braucht vielleicht eine alte Version eines Pakets, Projekt B eine neue. Ohne Trennung würden sie sich in die Quere kommen. Mit je einer eigenen `venv` hat jedes Projekt seine eigene saubere Werkbank.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Thema | Python | PHP |
    |---|---|---|
    | Pakete pro Projekt | `venv` + `pip install` | `composer require` + `vendor/` |
    | Abhängigkeiten festhalten | `requirements.txt` | `composer.json` / `composer.lock` |
    | Paket installieren | `pip install requests` | `composer require vendor/package` |

### venv anlegen

Im Projektordner (im Terminal):

```bash
python -m venv venv
```

Das erstellt einen Unterordner `venv/`. Den musst du nur **einmal pro Projekt** anlegen.

### venv aktivieren

=== "Windows (PowerShell)"

    ```powershell
    .\venv\Scripts\Activate.ps1
    ```

=== "macOS / Linux"

    ```bash
    source venv/bin/activate
    ```

Danach steht **`(venv)`** vorne in der Terminalzeile – die Umgebung ist aktiv.

### Pakete mit pip installieren

`pip` ist Pythons Paket-Installer. Beispiel:

```bash
pip install requests
```

Auflisten, was installiert ist:

```bash
pip list
```

### venv wieder verlassen

```bash
deactivate
```

!!! warning "Häufiger Fehler unter Windows: PowerShell blockiert das Skript"
    Meldung: `... Activate.ps1 cannot be loaded because running scripts is disabled on this system.`

    → Einmalig in PowerShell ausführen und mit `J`/`A` bestätigen:

    ```powershell
    Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
    ```

    Danach die Aktivierung erneut versuchen.

!!! tip "Ist die venv aktiv?"
    Vor jedem `pip install` prüfen, ob `(venv)` vorne in der Zeile steht. Fehlt es, landen Pakete global statt im Projekt.

---

## 2.5 Hello World – dein erstes Programm

### 1. Datei anlegen

In VS Code im Explorer eine neue Datei **`hallo.py`** erstellen.

### 2. Code schreiben

```python
print("Hallo, Welt!")
```

### 3. Ausführen

Im Terminal:

```bash
python hallo.py
```

### 4. Ausgabe prüfen

```
Hallo, Welt!
```

!!! info "Was passiert hier?"
    `print()` gibt den Text in den runden Klammern auf dem Bildschirm aus. Die **Anführungszeichen** machen aus dem Inhalt einen **Text** (einen „String").

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Python | PHP |
    |---|---|
    | `print("Hallo, Welt!")` | `echo "Hallo, Welt!";` |
    | `python hallo.py` | `php hallo.php` |

    Beides sind **Konsolen-Skripte**. PHP im Browser (`http://...`) braucht zusätzlich einen Webserver – Python-Skripte nicht.

??? info "Häufig gefragt: Muss ich auf den grünen ▶-Pfeil klicken oder ins Terminal tippen?"
    Beides geht. Der ▶-„Run"-Button oben rechts in VS Code führt die Datei aus und ist bequem. Den Terminal-Befehl `python hallo.py` solltest du trotzdem kennen – so startet man Programme „echt", und es funktioniert überall, auch ohne VS Code.

??? warning "Häufige Fehler beim ersten Programm"
    **`SyntaxError: unterminated string literal`** → Ein Anführungszeichen fehlt, z. B. `print("Hallo)`.

    **`can't open file 'hallo.py': No such file or directory`** → Du bist im falschen Ordner. Prüfe mit `ls` (macOS/Linux) bzw. `dir` (Windows), ob die Datei hier liegt, oder starte das Terminal im Projektordner.

    **`print` ohne Klammern** (`print "Hallo"`) → Das war Python 2. In Python 3 **immer mit Klammern**: `print("Hallo")`.

---

## 2.6 Typischer Projektaufbau

```
mein-projekt/
├── venv/              # Virtuelle Umgebung (gehört nicht ins Git)
├── hallo.py           # Dein Skript
├── requirements.txt   # Liste der installierten Pakete (optional)
└── README.md          # Kurzbeschreibung
```

Liste der Pakete erzeugen bzw. später woanders wiederherstellen:

```bash
pip freeze > requirements.txt      # speichern, welche Pakete installiert sind
pip install -r requirements.txt    # auf einem anderen Rechner alles nachinstallieren
```

---

## Kurzübungen

{{ task(file="tasks/tag2_01.yaml") }}

{{ task(file="tasks/tag2_02.yaml") }}

{{ task(file="tasks/tag2_03.yaml") }}
