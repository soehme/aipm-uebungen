# CLAUDE.md

## Language

Repo language: German. Conversation language: German (Du-Ton). Code language: English.
Edit this to change — trainees set their own here.

## Context

PM knowledge base for product "LeihsDir!". Consolidates customers, users, competitors,
market, experiments, strategy, roadmap, delivery, releases, user stories, process —
eventually codebase. Goal: derive decisions directly from accumulated context.
Growing set of connectors planned (Confluence, Jira, Miro, Slack, etc.) — currently
local files only.

Product context (`leihsdir-context.md`) lives in the setup-guide repo, not here.

## File organization

- Features: `feature/[name]/feature-[name].md`
- User stories: `feature/[feature-name]/story-[name].md`
- Competitors: `wettbewerber/wettbewerber-[name].md`; overview in `wettbewerber/wettbewerber.md`
- Research: `research/[topic].md`
- Meeting notes: `meetingnotes/YYYY-MM-DD-[topic].md`

Rules: lowercase, hyphens, German nouns for product docs, descriptive names (no `notes.md`, `doc1.md`).

Don't add top-level folders speculatively (market, strategy, roadmap, delivery, etc.).
Add one only once matching content actually recurs, following the same convention.

## Vocabulary (LeihsDir!)

### Correct terms
- **Leihende:r** / **Verleihende:r** (not "Nutzer A/B", "Borrower/Lender")
- **Nachbarschaft** (not "Community", "Neighborhood")
- **Werkzeug** / **Gerät** (not "Item", "Tool")
- **verSICHERt** — name of the insurance feature
- **Pic & Done** — name of the photo-upload feature
- **superlokal** (500m radius concept)

### Avoid these terms
- "Marketplace" (implies commercial focus — this is community-first)
- "Monetization" / "Revenue optimization" (conflicts with non-profit mission)
- "Users" (too impersonal — use Leihender/Verleihender)
- "Growth hacking" / "Viral loops" (wrong mindset for neighborhood trust)
- English product terms (target market is Germany)

Mix: German for product concepts/user-facing content, English OK for technical terms.
