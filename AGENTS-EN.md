## Language

Repo language: English. Conversation language: English (friendly, informal tone). Code language: English.
Edit this to change — trainees set their own here.

## Context

PM knowledge base for product "LeihsDir!" (alias: "BorrowIt" — both names mean the same product).
Consolidates customers, users, competitors, market, experiments, strategy, roadmap, delivery,
releases, user stories, process — eventually codebase. Goal: derive decisions directly from
accumulated context. Growing set of connectors planned (Confluence, Jira, Miro, Slack, etc.) —
currently local files only.

Product context (`leihsdir-context.md`) lives in the setup-guide repo, not here. It is written
in German — see "Translation guide" below.

## File organisation

- Features: `feature/[name]/feature-[name].md`
- User stories: `feature/[feature-name]/story-[name].md`
- Competitors: `competitors/competitor-[name].md`; overview in `competitors/competitors.md`
- Research: `research/[topic].md`
- Meeting notes: `meetingnotes/YYYY-MM-DD-[topic].md`

Rules: lowercase, hyphens, English nouns for product docs, descriptive names (no `notes.md`, `doc1.md`).

Don't add top-level folders speculatively (market, strategy, roadmap, delivery, etc.).
Add one only once matching content actually recurs, following the same convention.

## Vocabulary (LeihsDir!)

### Correct terms
- **borrower** / **lender** (not "user A/B", "renter/owner", "customer/seller")
- **neighbourhood** (not "community", "network")
- **tool** / **equipment** (not "item", "product", "listing")
- **inSUREed** — name of the insurance feature
- **Pic & Done** — name of the photo-upload feature
- **hyperlocal** (500 m radius concept)

### Avoid these terms
- "Marketplace" (implies commercial focus — this is community-first)
- "Monetisation" / "Revenue optimisation" (conflicts with non-profit mission)
- "Users" (too impersonal — use borrower/lender)
- "Growth hacking" / "Viral loops" (wrong mindset for neighbourhood trust)
- Other translations of feature names ("Insured", "Photo Upload", ...) — use the names above exactly

Target market is Germany. Everything is written in English for this training; product and
feature names stay as listed.

## Translation guide

The original case study and product context are German. This version was translated.
Source material (`leihsdir-context.md`, existing files and, if one was not translated, a skill
in `skills/`) can still use German names, concepts, folder paths and headings. When you read or
apply it, map to English and use only the English term in everything you write.

### Terms

| German | English |
|---|---|
| Leihende:r, Leihender, Ausleihende | borrower |
| Verleihende:r, Verleihender, Verleiher | lender |
| Nutzer | borrower or lender, depending on role |
| Nachbarschaft | neighbourhood |
| Nachbarn | neighbours |
| Werkzeug, Gerät, Gegenstand | tool, equipment |
| verSICHERt, (ver)SICHER(t) | inSUREed |
| Pic & Done | Pic & Done (unchanged) |
| superlokal | hyperlocal |
| LeihsDir! | LeihsDir! (alias BorrowIt) |
| Wettbewerber | competitor |
| Marktplatz | avoid; say "two-sided platform" when describing the cold-start problem |

### Paths and skills

| German (if a skill or file still uses it) | English (use this) |
|---|---|
| `wettbewerber/` | `competitors/` |
| `wettbewerber/wettbewerber.md` | `competitors/competitors.md` |
| `wettbewerber/wettbewerber-[name].md` | `competitors/competitor-[name].md` |
| `meetingnotes/YYYY-MM-DD-aenderungen.md` | `meetingnotes/YYYY-MM-DD-changes.md` |
| Overview table header `Name \| Gefunden am \| Datei` | `Name \| Found on \| File` |
| Competitor file headings `Kurzbeschreibung`, `Gemeinsamkeiten`, `Unterschiede zu LeihsDir`, `Business Model` | `Short description`, `Similarities`, `Differences from LeihsDir`, `Business model` |

`feature/`, `research/` and `meetingnotes/` are the same in both languages.

The main directory `leihsdir/` keeps exactly this name, also in English (never `borrowit/`,
the alias applies to the product name only). Everything below it is English.

### Rules

- Skills should be written in English and use the English paths and terms from this file.
- If a skill is still written in German, follow its steps, but apply the mappings above to
  paths, headings, table headers and output.
- Write all generated content in English, even where a skill's template or instructions are German.
- Web searches stay on the German market (competitor skill: tool and equipment rental in Germany).
  Use German search terms (e.g. "Werkzeug leihen", "Geräteverleih") and report findings in English.
- Where a skill points to the vocabulary in `CLAUDE.md`, use the vocabulary section of this file.
- If a German-named folder or file already exists, use it instead of creating the English
  counterpart next to it, and tell me.
- If I use a German term, answer with the English one.
