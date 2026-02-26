---
description: "Analysiert Git-Änderungen seit einem Datum und erstellt eine PM-gerechte Zusammenfassung"
---

Analysiere die Git-Änderungen in diesem Repository seit dem angegebenen Datum.

**Eingabe:** $ARGUMENTS (Format: YYYY-MM-DD, z.B. 2025-01-15). Falls kein Datum angegeben wurde, frage danach.

**Ablauf:**

1. Überprüfe mit `git log --oneline --since="DATUM"`, ob es Commits gibt. Falls keiner, teile das kurz mit.

2. Hole alle Commits seit dem Datum:
   git log --since="DATUM" --pretty=format:"%h %ad %s" --date=short

3. Hole die geänderten Dateien pro Commit:
   git log --since="DATUM" --name-status --pretty=format:"--- %h %s"

4. Hole eine Gesamtübersicht der geänderten Dateien:
   git diff --stat HEAD $(git log --since="DATUM" --pretty=format:"%H" | tail -1)^
   Falls nur ein Commit existiert, nutze: git show --stat

5. Fasse zusammen – nicht technisch, sondern aus PM-Perspektive:

   ## Zusammenfassung: Änderungen seit [DATUM]

   **[X] Commits** von [Datum] bis heute

   ### Was wurde geändert?
   Gruppiere Änderungen nach Thema/Bereich (basierend auf Dateipfaden und Commit-Messages).
   Erkläre in 2-3 Sätzen, was sich inhaltlich verändert hat.

   ### Betroffene Bereiche
   Liste die betroffenen Bereiche auf – keine technischen Pfade, sondern verständliche Benennung
   (z.B. "Dokumentation", "Tests", "Konfiguration").

   ### Wichtigste Einzeländerungen
   Top 3-5 Änderungen, die inhaltlich relevant sind. Je 1 Satz.

   ### Hinweise / Offene Fragen
   Falls etwas unklar ist oder auffällt (z.B. viele unkommentierte Änderungen,
   Löschungen von Dateien), erwähne es kurz.