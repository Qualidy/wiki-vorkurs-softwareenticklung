# Kapitel 1 – Einführung in Python

<div class="kurs-progress">
  <div class="step active"></div>
  <div class="step"></div>
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

- Was Programmieren überhaupt bedeutet – in einfachen Worten
- Wofür Python in der Praxis eingesetzt wird
- Warum Python die ideale Sprache für den Einstieg ist
- Was Python von einer Sprache wie C unterscheidet – und wann was sinnvoll ist
- Wie dieser Vorkurs über fünf Tage aufgebaut ist
</div>

---

<div class="anknuepfung" markdown>
<span class="ank-label">Wiederholung & Anknüpfung</span>
**Das kennst du schon** aus dem ersten Kursteil: den Einstieg in Python, den Vergleich Python ↔ C sowie die Vor- und Nachteile der Sprache.

**Neu / hier wichtig:** Wir ordnen alles in den 5-tägigen Vorkurs ein und schaffen eine gemeinsame Startlinie. Nutze dieses Kapitel als kurze Auffrischung und zum Nachschlagen – die volle Tiefe folgt bei den neuen Themen (Module, Dateien, Automationen).
</div>

## So gehst du vor

1. Lies dieses Kapitel in Ruhe – hier geht es um **Verstehen**, noch nicht ums Tippen.
2. Präg dir die fett markierten **Kernbegriffe** ein, sie kommen immer wieder vor.
3. Boxen mit **„Optional: Kennst du schon PHP?"** kannst du ignorieren, wenn du PHP nicht kennst.
4. Bearbeite am Ende die **Kurzübungen** – vom Einstieg bis zum kniffligeren Fall.
5. Schreib dir Fragen auf. Im nächsten Kapitel richten wir die Arbeitsumgebung ein und schreiben das erste Programm.

---

## 1.1 Was bedeutet „Programmieren"?

**Programmieren** heißt: einem Computer eine Aufgabe so genau beschreiben, dass er sie **selbstständig und beliebig oft** ausführen kann. Du sagst dem Computer nicht *„denk dir was aus"*, sondern gibst ihm eine **exakte Schritt-für-Schritt-Anleitung** – ähnlich einem Kochrezept.

Ein Beispiel aus dem Alltag, in Worten:

1. Frage den Benutzer nach seinem Namen.
2. Speichere die Antwort.
3. Gib „Hallo" + den Namen auf dem Bildschirm aus.

Genau diese drei Schritte sehen in Python so aus:

```python
name = input("Wie heißt du? ")
print("Hallo, " + name + "!")
```

Wichtig ist die Denkweise: Programmieren ist **kein Auswendiglernen von Befehlen**, sondern **Probleme in kleine, logische Schritte zerlegen**. Die Befehle schlägst du anfangs ständig nach – das ist völlig normal und bleibt auch bei Profis so.

!!! info "Warum „Anweisungen", nicht „Wünsche"?"
    Ein Computer macht **exakt das**, was im Code steht – nicht das, was du *gemeint* hast. Tippfehler, ein vergessenes Anführungszeichen oder eine falsche Reihenfolge führen sofort zu einer Fehlermeldung. Das ist kein Drama, sondern normaler Arbeitsalltag: Fehler lesen, verstehen, korrigieren.

---

## 1.2 Wofür wird Python benutzt?

Python ist eine **Allzweck-Sprache** – man kann damit sehr unterschiedliche Dinge bauen:

| Bereich | Wofür konkret? | Bekannte Beispiele |
|---|---|---|
| Webentwicklung | Server/Backend von Websites und Apps | Instagram, Spotify |
| Datenanalyse | Tabellen auswerten, Diagramme erstellen | Reports, Dashboards |
| Künstliche Intelligenz | Modelle trainieren, Bilderkennung | ChatGPT-Umfeld, Forschung |
| Automatisierung | Wiederkehrende Aufgaben am PC abnehmen | Dateien sortieren, Daten bereinigen |
| Technik & Wissenschaft | Messdaten auswerten, Simulationen | NASA, Forschungslabore |

In **diesem Vorkurs** liegt der Schwerpunkt auf den **Grundlagen** und am Ende auf **kleinen Automationen** – also genau den kleinen Helfer-Skripten, die im Berufsalltag am häufigsten gebraucht werden.

??? info "Häufig gefragt: Brauche ich Mathe, um programmieren zu können?"
    Für den Einstieg reichen die **vier Grundrechenarten**. Logisches, sauberes Denken ist wichtiger als höhere Mathematik. In diesem Vorkurs geht es um **Programmieren in Python** – nicht um Mathe-Übungen.

---

## 1.3 Warum ausgerechnet Python für den Einstieg?

### Der Code liest sich fast wie Englisch

Python wurde bewusst so entworfen, dass Code **gut lesbar** ist. Es gibt wenig „Drumherum" und keine geschweiften Klammern für Codeblöcke. Vergleiche dieselbe Aufgabe – Name abfragen und begrüßen – in zwei Sprachen:

**Python:**

```python
name = input("Wie heißt du? ")
print(f"Hallo, {name}!")
```

**C** (eine klassische, hardwarenahe Sprache – hier nur ein Ausschnitt):

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char name[100];
    printf("Wie heißt du? ");
    fgets(name, 100, stdin);
    name[strcspn(name, "\n")] = '\0';   /* Zeilenumbruch entfernen */
    printf("Hallo, %s!\n", name);
    return 0;
}
```

Beides macht dasselbe. In Python brauchst du **2 Zeilen**, in C deutlich mehr und musst dich um Details wie Speicherreservierung kümmern. Für den Einstieg ist die Python-Variante klar im Vorteil.

??? info "Optional: Kennst du schon PHP?"
    Nur relevant, wenn du **PHP schon kennst** – sonst einfach überspringen.

    | Thema | Python | PHP |
    |---|---|---|
    | Ausgabe | `print(f"Hallo {name}")` | `echo "Hallo $name";` |
    | Variable | `name = "Anna"` | `$name = "Anna";` |
    | Codeblöcke | **Einrückung** (Kapitel 5) | `{ ... }` |
    | Syntax | kein `$`, kein `;` | `$` und `;` üblich |

    Python-Skripte startest du in der Konsole mit `python datei.py` – vergleichbar mit `php datei.php`, nur ohne Webserver.

### Weitere Pluspunkte

- **Riesige Auswahl an fertigen Bausteinen** (Bibliotheken), die du dir dazuholen kannst – du musst nicht alles selbst bauen.
- **Große Community**: Zu fast jedem Problem findest du eine Antwort online.
- **Plattformunabhängig**: Derselbe Code läuft auf Windows, macOS und Linux.

---

## 1.4 Python ist nicht für alles perfekt

Damit du es richtig einordnen kannst – Python hat auch Grenzen:

| Eigenschaft | Bedeutung im Alltag |
|---|---|
| Eher langsam | Python wird Zeile für Zeile ausgeführt (**interpretiert**). Für die meisten Aufgaben völlig ausreichend, für Hochleistungs-Software nicht ideal. |
| Höherer Speicherbedarf | Python braucht mehr Arbeitsspeicher als z. B. C. |
| Externe Abhängigkeiten | Viele Projekte nutzen Zusatzpakete, die man verwalten muss (Kapitel 2). |

!!! tip "Merksatz"
    **Für Einstieg, Skripte, Datenauswertung und Automatisierung ist Python ideal.** Für extrem schnelle, hardwarenahe Systeme (z. B. Steuerung von Mikrocontrollern) ist eine Sprache wie C oft besser. Beides schließt sich nicht aus – wer Python kann, lernt später jede andere Sprache leichter.

---

## 1.5 „Interpretiert" vs. „kompiliert" – kurz erklärt

Du wirst die Begriffe immer wieder hören:

- **Interpretiert (Python):** Ein Programm namens **Interpreter** liest deinen Code und führt ihn **direkt** aus – Zeile für Zeile. Vorteil: sofort ausprobieren, kein Zwischenschritt.
- **Kompiliert (z. B. C):** Der Code wird zuerst von einem **Compiler** komplett in Maschinensprache übersetzt. Erst danach läuft das fertige Programm – dafür sehr schnell.

| | Python (interpretiert) | C (kompiliert) |
|---|---|---|
| Ausführung | Direkt, Zeile für Zeile | Erst übersetzen, dann ausführen |
| Geschwindigkeit | Gut genug für die meisten Fälle | Sehr schnell |
| Lesbarkeit | Sehr hoch | Geringer, mehr Details |
| Einstieg | Ideal für Anfänger | Steiler |

---

## 1.6 Aufbau des Vorkurses

Der Vorkurs läuft über **5 Tage** mit je **2 Kapiteln**:

| Tag | Kapitel | Schwerpunkt |
|---|---|---|
| 1 | 1–2 | Einordnung & Arbeitsumgebung einrichten |
| 2 | 3–4 | Textverarbeitung & Python-Grundlagen |
| 3 | 5–6 | Entscheidungen (`if`) & Wiederholungen (Schleifen) |
| 4 | 7–8 | Funktionen, Module & Dateien |
| 5 | 9–10 | Automationen & Datenstrukturen |

Was du mitbringen solltest:

- Einen Laptop oder Computer
- Lust, Dinge selbst auszuprobieren (am meisten lernst du durch **Tippen**, nicht durch Zuschauen)
- Geduld mit Fehlermeldungen – sie sind dein wichtigstes Lernwerkzeug

??? info "Häufig gefragt: Was, wenn ich noch nie eine Zeile Code geschrieben habe?"
    Genau dafür ist dieser Vorkurs gemacht. Wir starten bei Null. Jedes neue Konzept wird an einem kleinen, lauffähigen Beispiel gezeigt. Wenn etwas unklar ist: ausprobieren, verändern, schauen was passiert – kaputtmachen kann man dabei nichts.

---

## Kurzübungen

{{ task(file="tasks/tag1_01.yaml") }}

{{ task(file="tasks/tag1_02.yaml") }}

{{ task(file="tasks/tag1_03.yaml") }}
