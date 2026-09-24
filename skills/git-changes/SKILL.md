---
name: git-changes
description: >
  Fasst die Git-Änderungen eines Repositories seit einem Stichtag PM-gerecht zusammen:
  Themen, betroffene Bereiche, wichtigste Einzeländerungen. Nutze diesen Skill wenn jemand
  wissen will, was sich seit einem Datum im Repo geändert hat, ein Änderungs-Update,
  einen Wochenrückblick oder eine Commit-Zusammenfassung braucht.
  Trigger-Phrasen: Was hat sich geändert, Änderungen seit, Git-Zusammenfassung,
  Commit-Übersicht, Was ist letzte Woche passiert.
argument-hint: "[datum oder zeitraum]"
---

# Git-Änderungen zusammenfassen

Lies die Commit-Historie dieses Repositories ab einem Stichtag und fasse sie so zusammen,
dass eine Produktmanagerin ohne Git-Kenntnisse versteht, was inhaltlich passiert ist.

## Stichtag bestimmen

- Konkretes Datum in der Anfrage (`2025-01-15`, `15.01.2025`) → direkt verwenden.
- Relative Angabe ("letzte Woche", "seit gestern", "seit dem Workshop am Dienstag") →
  in ein konkretes Datum `YYYY-MM-DD` umrechnen.
- Nichts genannt → die letzten 7 Tage nehmen, nicht nachfragen.

Nenne den aufgelösten Stichtag immer in der Ausgabe. Alle Kommandos unten verwenden
ihn an der Stelle `DATUM`.

## Ablauf

### 1. Ist das überhaupt ein Git-Repo?

```
git rev-parse --is-inside-work-tree
```

Schlägt das fehl: Ausgabe in Alltagssprache statt der git-Fehlermeldung — dieser Ordner
wird nicht von Git versioniert, es gibt also keine Änderungshistorie. Danach abbrechen.

### 2. Umfang prüfen

```
git log --oneline --since="DATUM" | wc -l
```

- **0 Commits** → kurz mitteilen, dass im Zeitraum nichts committet wurde. Trotzdem noch
  Schritt 5 (uncommittete Änderungen) laufen lassen, danach abbrechen.
- **1 bis 40 Commits** → Schritt 3 (Detailvariante).
- **mehr als 40 Commits** → Schritt 4 (Kompaktvariante). Sonst wird die Ausgabe zu lang.

### 3. Detailvariante

```
git log --since="DATUM" --no-merges --date=short --pretty=format:"=== %h | %cd | %an | %s" --name-status
```

Das enthält Commits, Daten, Autor:innen und geänderte Dateien in einem Durchgang.
Kein weiteres Kommando nötig.

### 4. Kompaktvariante (viele Commits)

```
git log --since="DATUM" --no-merges --date=short --pretty=format:"%h | %cd | %s"
git log --since="DATUM" --no-merges --name-only --pretty=format: | grep -v '^$' | sort | uniq -c | sort -rn | head -30
```

Für den Gesamtumfang zusätzlich den Basis-Commit bestimmen:

```
git rev-list -1 --before="DATUM" HEAD
```

Liefert das einen Commit-Hash, dann — mit dem Hash eingesetzt, nicht als
Command-Substitution:

```
git diff --stat <hash> HEAD
```

Liefert es **nichts**, beginnt die Historie erst nach dem Stichtag. Dann kein `git diff`
aufrufen, sondern das im Bericht vermerken ("Historie beginnt am …") und den Umfang aus
der Dateiliste ableiten.

### 5. Uncommittete Änderungen

```
git status --short
```

Diese Änderungen sind **nicht** Teil der Historie. Wenn welche existieren, am Ende
separat erwähnen — sonst wundern sich Leser:innen, warum ihre Arbeit von gestern fehlt.

## Betroffene Bereiche benennen

Übersetze Ordner in Klartext, statt Pfade auszugeben:

| Pfad | Bezeichnung im Bericht |
|---|---|
| `feature/` | Features und User Stories |
| `wettbewerber/` | Wettbewerbsbeobachtung |
| `research/` | Recherchen |
| `meetingnotes/` | Meeting-Notizen |
| `skills/` | Automatisierungen für den KI-Assistenten |
| `CLAUDE.md`, `AGENTS.md` | Arbeitsanweisungen für den KI-Assistenten |
| alles andere | nach Ordnernamen sinngemäß benennen |

## Ausgabeformat

Bei **mehr als 3 Commits** die volle Struktur:

```markdown
## Änderungen seit [DATUM]

**[X] Commits** von [ältestes Datum] bis [jüngstes Datum]

### Kurzfassung
[2-3 Sätze: was inhaltlich passiert ist. Keine Dateinamen, keine Commit-Hashes.]

### Themen
[Pro Thema eine Überschriftenzeile in Fettschrift, darunter 1-2 Sätze.
Betroffene Bereiche in Klartext (siehe Tabelle), Dateinamen nur wenn sie
für sich sprechen.]

### Auffälligkeiten
[Nur wenn es etwas zu sagen gibt: gelöschte Inhalte, nichtssagende Commit-Messages,
ein Bereich der auffällig oft angefasst wurde, ein langer Zeitraum ohne Aktivität.
Nichts Auffälliges → Abschnitt weglassen.]
```

Bei **1 bis 3 Commits**: nur Kurzfassung plus eine Liste mit je einem Satz pro Commit.
Die volle Struktur wäre überdimensioniert.

## Regeln

- **Keine Kommandos erfinden.** Nur die oben genannten. Insbesondere kein
  `git diff HEAD <commit>^` — die Reihenfolge dreht den Diffstat um und `^` scheitert
  am ersten Commit eines Repos.
- **Inhalt vor Mechanik.** Nicht "12 Dateien geändert, 340 Zeilen hinzugefügt", sondern
  was sich inhaltlich verändert hat. Zahlen höchstens als Randnotiz.
- **Nichts dazuerfinden.** Was aus Commit-Message und Dateinamen nicht hervorgeht, bleibt
  offen — dann lieber "unklar, was dahintersteckt" als eine plausible Vermutung, die als
  Fakt gelesen wird.
- **LeihsDir-Vokabular** aus der CLAUDE.md gilt auch hier: Leihende:r / Verleihende:r,
  Nachbarschaft, Werkzeug. Kein "Users", kein "Marketplace".
- **Nichts schreiben.** Der Skill liest nur und gibt die Zusammenfassung im Chat aus.
  Soll sie als Datei abgelegt werden, danach fragen und nach
  `meetingnotes/YYYY-MM-DD-aenderungen.md` speichern.
- Keine Emojis, keine Füllwörter, kein Git-Jargon in der Ausgabe (kein "Branch",
  "Merge", "Staging" ohne Erklärung).
