---
name: user-story-skill
description: "Generiert strukturierte User Stories mit starkem Fokus auf Motivation (Warum?), Metriken (IST/SOLL) und Appetit (Shape-Up + Kano). Nutze diesen Skill wenn jemand eine User Story, ein Feature-Template, oder eine Story mit Akzeptanzkriterien und Gherkin-Testcases erstellen möchte. Trigger-Phrasen: User Story schreiben, Story generieren, Feature beschreiben, Story Template ausfüllen."
---
# User Story Skill

Erstelle strukturierte User Stories aus konkreten Feature-Beschreibungen.

## Dein Kernprinzip

**Das "Wozu?" kommt VOR dem "Was".** Jede Story beginnt mit der Motivation und den Metriken–nicht mit der Lösung. Erst wenn klar ist, WARUM wir etwas bauen und WORAN wir Erfolg messen, beschreiben wir WAS gebaut werden soll.

## Input

Du bekommst eine konkrete Feature-Beschreibung oder Produktidee. Daraus generierst du eine vollständige User Story im folgenden Template.

Falls zum Produkt eine Case Study oder Produktbeschreibung existiert, nutze diese als Kontext für realistische Metriken und Szenarien.

## Template

Generiere die Story exakt in dieser Struktur:

---

### Story: {Konkreter, beschreibender Feature-Titel}

KEIN "Als x möchte ich y um z"-Format. Der Titel beschreibt das Feature klar und konkret.

---

### 1. Motivation (Why?) `[PM]`

> **Wozu bauen wir das?**

{2-4 Sätze im Hypothesen-Stil. Wir formulieren unsere ANNAHMEN, nicht Fakten.
Sprachliche Marker:
- "Wir glauben, dass..."
- "Unsere Annahme ist..."
- "Wir haben Grund zur Annahme, dass... weil..."
- "Wenn wir falsch liegen, würden wir sehen, dass..."

Erkläre:
- Welches Nutzerproblem vermuten wir?
- Warum glauben wir, dass es jetzt wichtig ist?
- Was passiert vermutlich, wenn wir es NICHT bauen?

Wichtig: Ehrlich sein über Unsicherheit. Alles hier ist Hypothese–fundiert, aber falsifizierbar.}

**Strategischer Bezug:** {Auf welches Produktziel / welche Vision zahlt dieses Feature ein?}

---

### 2. Metriken `[PM]`

> **Woran erkennen wir, dass das Feature bei Nutzenden ankommt?**

Sortierung: Zuerst sofort erlebbare und ohne Verzögerung messbare Metriken, dann nachgelagerte Impact-Metriken.

**Sofort messbar (ab Tag 1):**

| Metrik | IST (heute) | SOLL (nach Release) | Messzeitpunkt |
|--------|-------------|---------------------|---------------|
| {Verhaltensmetrik 1–sofort beobachtbar} | {aktueller Wert} | {erwarteter Zielwert} | {ab Release} |
| {Verhaltensmetrik 2–sofort beobachtbar} | {aktueller Wert} | {erwarteter Zielwert} | {ab Release} |

**Nachgelagert (Impact):**

| Metrik | IST (heute) | SOLL (nach Release) | Messzeitpunkt |
|--------|-------------|---------------------|---------------|
| {Impact-Metrik–braucht Zeit} | {aktueller Wert} | {erwarteter Zielwert} | {z.B. 8 Wochen nach Release} |

**Guardrail-Metrik:** {Was darf sich durch das Feature NICHT verschlechtern?}

---

### 3. Appetit `[PM]`

> **Wie viel Zeit ist es uns wert?**

**Appetit:** {1 Woche | 2 Wochen | 6 Wochen}

**Kano-Kategorie:** {Basis-Merkmal | Leistungs-Merkmal | Begeisterungs-Merkmal}

**Begründung:**
{1-2 Sätze, die den Appetit mit der Kano-Kategorie verbinden. Beispiele:

- Basis-Merkmal → "Ohne dieses Feature ist das Produkt nicht nutzbar. Wir investieren bis zu X Wochen, weil es eine Grundvoraussetzung ist."
- Leistungs-Merkmal → "Je besser wir das lösen, desto zufriedener die Nutzer. X Wochen sind angemessen für den erwarteten Impact auf {Metrik}."
- Begeisterungs-Merkmal → "Nutzer erwarten das nicht, aber es differenziert uns. Maximal X Wochen–wenn es länger dauert, ist der Überraschungseffekt den Aufwand nicht wert."}

---

### 4. Description (Was) `[PM + Team]`

{Beschreibung der Lösung in 3-8 Sätzen:
- Was soll gebaut werden?
- Wie soll es sich für den Nutzer anfühlen?
- Was gehört explizit NICHT dazu (Scope-Abgrenzung)?}

**In Scope:**
- {Element 1}
- {Element 2}
- {Element 3}

**Out of Scope:**
- {Was bewusst nicht enthalten ist}

---

### 5. Acceptance Criteria `[PM + Team]`

- [ ] {Kriterium 1–beobachtbares Verhalten aus Nutzersicht}
- [ ] {Kriterium 2}
- [ ] {Kriterium 3}
- [ ] {Kriterium 4}
- [ ] {Edge Case / Fehlerfall}

---

### 6. Testcases `[während Bearbeitung – jede:r]`

```gherkin
Feature: {Feature-Name}

  Scenario: {Happy Path}
    Given {Ausgangszustand}
    When {Aktion des Nutzers}
    Then {Erwartetes Ergebnis}

  Scenario: {Wichtiger Alternativpfad}
    Given {Ausgangszustand}
    When {Abweichende Aktion}
    Then {Erwartetes Ergebnis}

  Scenario: {Fehlerfall / Edge Case}
    Given {Problematischer Zustand}
    When {Aktion des Nutzers}
    Then {Fehlerbehandlung}
```

---

## Regeln für die Generierung

### Motivation (Sektion 1)
- IMMER im Hypothesen-Stil formulieren: "Wir glauben...", "Unsere Annahme ist..."
- NIEMALS als Fakt darstellen–alles hier ist unsere beste Einschätzung, die falsch sein kann
- Das Nutzerproblem beschreiben, nie die Lösung
- "Was passiert wenn wir es NICHT bauen?" ist Pflicht im Kopf–es zwingt zur Ehrlichkeit
- Strategischer Bezug muss konkret sein, nicht "verbessert die User Experience"

### Metriken (Sektion 2)
- **Sortierung: Sofort messbar VOR nachgelagert.** Erst Verhaltensmetriken (Abbruchrate, Klicks, Nutzungen pro Session), dann Impact-Metriken (Retention, durchschnittliche Nutzung über Zeit)
- Outcome-Metriken, KEINE Output-Metriken ("Nutzer-Retention" statt "Feature deployed")
- IST-Werte dürfen geschätzt sein, aber niemals leer–lieber "~30% (geschätzt)" als nichts
- SOLL-Werte müssen ambitioniert aber realistisch sein
- Guardrail-Metrik schützt vor unbeabsichtigten Nebenwirkungen

### Appetit (Sektion 3)
- Immer Shape-Up-Zeiträume: 1 Woche, 2 Wochen, oder 6 Wochen
- Kano-Kategorie bestimmt die Denkrichtung:
  - **Basis:** Muss funktionieren, nicht überinvestieren
  - **Leistung:** Mehr Investment = mehr Zufriedenheit (linearer Zusammenhang)
  - **Begeisterung:** Klein halten, Überraschung > Perfektion
- Appetit ist ein BUDGET, kein Estimate. "So viel ist es uns wert" ≠ "So lange dauert es"

### Description (Sektion 4)
- Out of Scope ist genauso wichtig wie In Scope
- Lösungsbeschreibung, nicht Problembeschreibung (das war Sektion 1)

### Acceptance Criteria (Sektion 5)
- Beobachtbares Verhalten, keine technischen Implementierungsdetails
- Mindestens ein Edge Case / Fehlerfall

### Testcases (Sektion 6)
- Gherkin-Syntax (Given/When/Then)
- Mindestens 3 Scenarios: Happy Path, Alternativpfad, Fehlerfall
- Alltagssprache, keine technischen Details

## Tonalität

- Klar und direkt, keine Füllwörter
- Sprache des Produkts/der Nutzer verwenden, nicht Entwickler-Jargon
- Metriken konkret, nicht vage ("Conversion von 2% auf 5%" statt "Conversion verbessern")

## Checkliste (intern, nicht ausgeben)

Prüfe vor der Ausgabe:
- [ ] Kein "Als x möchte ich y um z"-Format–konkreter Feature-Titel
- [ ] Motivation ist im Hypothesen-Stil ("Wir glauben..."), nicht als Fakt
- [ ] Motivation erklärt das WARUM, nicht das WAS
- [ ] Metriken: Sofort messbare VOR nachgelagerten Impact-Metriken
- [ ] Mindestens 1 Outcome-Metrik mit IST und SOLL
- [ ] Guardrail-Metrik vorhanden
- [ ] Appetit passt zur Kano-Kategorie
- [ ] Description hat In Scope UND Out of Scope
- [ ] Acceptance Criteria sind aus Nutzersicht formuliert
- [ ] Mindestens 3 Gherkin-Scenarios
- [ ] `[PM]`, `[PM + Team]`, `[während Bearbeitung – jede:r]` Tags sind gesetzt