---
name: wettbewerbsmonitoring
description: >
  Führt ein regelmäßiges Wettbewerbsmonitoring durch: Positionierungen pflegen, neue Wettbewerber
  identifizieren, News recherchieren (via Sub-Agents), Dossier erstellen. Universell einsetzbar –
  beim Erstlauf werden alle Informationen interaktiv abgefragt. Nutze diesen Skill wenn jemand
  Wettbewerber beobachten, ein Monitoring durchführen, oder ein Wettbewerbs-Dossier erstellen möchte.
triggers:
  - "Wettbewerbsmonitoring"
  - "Wettbewerbsanalyse"
  - "Wettbewerber beobachten"
  - "Monitoring durchführen"
  - "Competitor monitoring"
  - "Wettbewerbs-Dossier"
---

Führe ein regelmäßiges Wettbewerbsmonitoring gemäß beschriebener Schritte durch. Sollten Dateien oder Ordner nicht existieren, leg sie bitte an.

# PLATZHALTER

| Kürzel | Bedeutung |
|--------|-----------|
| `{WIR}` | Name unseres Unternehmens |
| `{WB}` | Name eines Wettbewerbers |
| `{HEUTE}` | Heutiges Datum als YYYY-MM-DD |

# PFADE

| Kurzname           | Pfad                                         |
| ------------------ | -------------------------------------------- |
| WIR-Positionierung | `wettbewerber/WIR/positionierung-{WIR}.md`   |
| WB-Positionierung  | `wettbewerber/{WB}/positionierung-{WB}.md`   |
| WB-News            | `wettbewerber/{WB}/news-{WB}.md`             |
| Wettbewerberliste  | `wettbewerber/wettbewerberliste.md`          |
| Dossier            | `wettbewerber/monitoring/dossier-{HEUTE}.md` |

Der Ordner `wettbewerber/WIR/` kennzeichnet immer das eigene Unternehmen. Der Ordnername ist fix, der Dateiname enthält den tatsächlichen Unternehmensnamen.

---

# SCHRITTE

## 0. Erstlauf-Erkennung

**Prüfe:** Existiert `wettbewerber/WIR/` mit einer Positionierungsdatei?

**Wenn NEIN (Erstlauf):**
1. Erfrage interaktiv beim Nutzer:
   - Unternehmensname
   - Branche und Produktkategorien
   - Zielmärkte (z.B. DACH, Europa, Global)
   - Strategischer Schwerpunkt
   - Bekannte Wettbewerber (falls vorhanden)
2. Erstelle daraus die **WIR-Positionierung** gemäß der Vorlage unten.
3. Erstelle die **Wettbewerberliste** mit dem eigenen Unternehmen und den genannten Wettbewerbern.
4. Mache Vorschläge für weitere Wettbewerber basierend auf Branche und Markt.

**Wenn JA:** → Weiter mit Schritt 1.

## 1. Unsere Positionierung verstehen

Lies die **WIR-Positionierung** mit Informationen zu unserem Unternehmen, den wichtigsten Produkten/Produktkategorien, Märkten und unserem strategischen Schwerpunkt.

## 2. Wettbewerber einlesen

Lies die **Wettbewerberliste**. Dort sind Wettbewerber mit Status gelistet:
- **include**–aktiv beobachten
- **exclude**–bewusst ignorieren
- **review**–noch einzusortieren

Auch wir selbst sind dort gelistet.

## 3. Neue Wettbewerber suchen

Suche nach neuen Marktteilnehmern (80/20–gründlich genug, aber nicht erschöpfend):
- Suche nach `"{Produktkategorie} Alternative"` und `"{Produktkategorie} Anbieter"` in der Sprache der Zielmärkte
- Suche nach `"Konkurrenz zu {WIR}"` bzw. `"{WIR} competitors"`
- Suche nach Vergleichsportalen und Marktübersichten (z.B. G2, Capterra, Trustpilot, branchenspezifische Verzeichnisse)
- Maximal 3–5 neue Kandidaten pro Durchlauf

Ergänze Funde in der **Wettbewerberliste** mit Status `review`.

## 4. Fehlende Positionierungen erstellen

Prüfe für jeden Wettbewerber mit Status `include`, ob eine **WB-Positionierung** existiert. Falls nicht, erstelle sie gemäß der Vorlage unten.

## 5. Neuigkeiten recherchieren

Starte für jeden Wettbewerber (und unser Unternehmen) einen Sub-Agent. Maximal 5 parallel, weitere sequentiell.

### 5a. Positionierung lesen
Lies die **WB-Positionierung** (bzw. **WIR-Positionierung** für unser Unternehmen).

### 5b. News recherchieren
Recherchiere aktuelle Neuigkeiten zum Unternehmen in folgenden Kategorien:
- Pressemitteilungen
- Website-Updates (Produktseiten, News-Bereich)
- Social Media des Unternehmens (LinkedIn, Twitter/X)
- Social Media und Interviews der Führungskräfte (LinkedIn, Twitter/X)
- Produkt-Launches & Ankündigungen
- Service-Erweiterungen
- Patente & Innovationen
- Awards & Auszeichnungen
- Messeauftritte & Events
- M&As und Partnerschaften

### 5c. Gegen bisherige News abgleichen
Vergleiche die Ergebnisse mit der **WB-News**-Datei. Siehe Regeln zur Deduplizierung.

### 5d. News dokumentieren
Ergänze neue Erkenntnisse in der **WB-News**-Datei unter der Überschrift `## {HEUTE}`.
Falls keine neuen Erkenntnisse: `Keine neuen Erkenntnisse im Recherchezeitraum.` eintragen.

## 6. Dossier erstellen

### 6a. Bisherige Dossiers lesen
Lies die letzten 8 **Dossiers** aus `wettbewerber/monitoring/` (oder weniger, falls weniger existieren).

### 6b. Neues Dossier schreiben
Erstelle ein neues **Dossier** mit Neuigkeiten, die in den letzten 8 Dossiers noch nicht berichtet wurden oder neue Relevanz erhalten haben.

**Struktur des Dossiers:**
1. Executive Summary
2. Findings pro Unternehmen (gruppiert nach Kategorie)
3. Neue Wettbewerber (falls gefunden)
4. Empfehlungen zum Handeln
5. Hinweise auf Recherche-Probleme (nicht erreichbare Quellen, veraltete Positionierungen)

**Relevanz-Bewertung:** ⭐ niedrig · ⭐⭐ mittel · ⭐⭐⭐ hoch

## 7. Zusammenfassung

Zeige dem Nutzer eine Zusammenfassung der wichtigsten Erkenntnisse.

---

# REGELN

## Deduplizierung
- Nur News aufnehmen, die **nach dem Datum der letzten Überschrift** in der WB-News-Datei liegen.
- Bereits berichtete News nur erneut aufnehmen, wenn es **substanzielle neue Entwicklungen** dazu gibt. Dann als `[Update]` kennzeichnen.

## Fehlerbehandlung
- **Website nicht erreichbar / Tool-Fehler:** In der WB-News-Datei dokumentieren als `⚠️ [Quelle] nicht erreichbar am {HEUTE}`. Im Dossier unter "Recherche-Probleme" erwähnen.
- **Keine News gefunden:** Explizit `Keine neuen Erkenntnisse im Recherchezeitraum.` eintragen–nicht einfach weglassen.
- **Veraltete Positionierung** (älter als 6 Monate): Im Dossier Hinweis auf Aktualisierungsbedarf geben.

## Quellen
- Nur verifizierte URLs verwenden, die tatsächlich aus WebSearch- oder WebFetch-Ergebnissen stammen.
- **Keine URLs erfinden.** Falls keine direkte Quelle verfügbar: Suchbegriff angeben, z.B. `(Quelle: WebSearch nach "[Suchbegriff]", {HEUTE})`

---

# VORLAGE

## Struktur für Unternehmensdarstellungen
Gilt für **WIR-Positionierung** und **WB-Positionierung**:

```markdown
# Positionierung {UNTERNEHMENSNAME}

## Grundlegende Informationen
### Unternehmensübersicht (Gründungsjahr, Größe, Standorte, Eigentümerstruktur)
### Geschäftsmodell & Umsatzquellen

## Markt & Positionierung
### Zielgruppen & Kundensegmente
### Positionierung & USPs (was behaupten sie, besser zu können?)
### Preismodell & Preisniveau

## Produkt & Leistung
### Produkte / Dienstleistungen im Überblick
### Stärken & Schwächen des Angebots
### Produktneuheiten & Entwicklungsrichtung

## Vertrieb & Marketing
### Vertriebskanäle
### Marketingstrategie & Kommunikation
### Online-Präsenz (Website, SEO, Social Media)
### Werbemaßnahmen & Kampagnen

## Kundenwahrnehmung
### Kundenbewertungen & Reputation
### Beschwerden & Schwachstellen (Chancen für dich!)

## Finanzen & Wachstum
### Umsatz/Wachstum (soweit öffentlich)
### Investitionen & Finanzierungsrunden
### Personalentwicklung (Stellenausschreibungen)

## Bewertung
### Wo sind sie besser als wir?
### Wo sind wir besser?
### Welche Bedrohung gehen von ihnen aus?
### Welche Chancen ergeben sich für uns?
```