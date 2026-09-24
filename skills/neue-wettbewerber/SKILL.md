---
name: neue-wettbewerber
description: >
  Sucht neue, noch nicht gelistete Wettbewerber zu LeihsDir im Bereich Werkzeug- und
  Geräteleihe in Deutschland, pflegt wettbewerber.md und legt je Fund eine Detaildatei
  an. Nutze diesen Skill wenn jemand neue Wettbewerber finden, die Wettbewerberliste
  aktualisieren oder ein Wettbewerber-Update durchführen möchte.
triggers:
  - "Neue Wettbewerber"
  - "Wettbewerber aktualisieren"
  - "Wettbewerber finden"
  - "Wettbewerberliste ergänzen"
---

# PFADE (fix)

| Kurzname          | Pfad                                    |
| ------------------ | ---------------------------------------- |
| Übersicht          | `wettbewerber/wettbewerber.md`           |
| Detail je Wettbewerber | `wettbewerber/wettbewerber-[name].md` (`[name]` = lowercase-hyphen) |

# SCHRITTE

## 1. Übersicht lesen
Existiert `wettbewerber/wettbewerber.md`? Nein → anlegen mit Kopfzeile:

```markdown
| Name | Gefunden am | Datei |
|------|-------------|-------|
```

## 2. Bestehende Namen extrahieren
Liste der schon gelisteten Wettbewerber ziehen. Schreibvarianten beachten (Groß-/Kleinschreibung, Leerzeichen/Bindestrich) — kein Duplikat durch reine Schreibweise.

## 3. Suchdurchgang
Ein WebSearch-Durchgang im Bereich Werkzeug- und Geräteleihe Deutschland. Finde bis zu **2 Kandidaten**, die noch NICHT gelistet sind.

Keine Kandidaten gefunden → weiter zu Schritt 6, das dort so vermerken. Keine Dateien anlegen.

## 4. Sub-Agents starten
Für jeden neuen Kandidaten (max. 2, parallel) einen Sub-Agent starten. Jeder Sub-Agent:
- recherchiert kurz zu genau einem Kandidaten
- schreibt `wettbewerber/wettbewerber-[name].md` nach der Vorlage unten
- keine weitere Rekursion (Sub-Agent startet selbst keine weiteren Sub-Agents)

## 5. Übersicht ergänzen
Nach Rückkehr der Sub-Agents: je neuem Wettbewerber eine Zeile in `wettbewerber/wettbewerber.md` ergänzen — Name, heutiges Datum (YYYY-MM-DD), Link zur Detaildatei.

## 6. Zusammenfassung
Zeige, was neu dazukam und was übersprungen wurde (bereits gelistet). Bei keinem Fund: das explizit so sagen, nicht leer lassen.

---

# REGELN

- **Cap 2 Kandidaten pro Lauf** — Zeitbudget vor Vollständigkeit.
- **Sub-Agents:** max. 2 parallel, je einer pro Kandidat, keine weitere Rekursion.
- **Keine erfundenen Fakten oder URLs.** Ohne verifizierte Quelle: Suchbegriff angeben statt Quelle zu erfinden.
- Dateinamen: lowercase-hyphen, kein Leerzeichen.

---

# VORLAGE

Gilt für `wettbewerber-[name].md`:

```markdown
# {Wettbewerbername}

## Kurzbeschreibung
{2-4 Sätze: was das Unternehmen macht}

## Gemeinsamkeiten
{2-4 Sätze: was ähnlich zu LeihsDir ist}

## Unterschiede zu LeihsDir
{2-4 Sätze: was konkret anders ist}

## Business Model
{2-4 Sätze: wie das Unternehmen Geld verdient}
```
