---
name: new-competitors
description: >
  Finds new competitors to LeihsDir (alias BorrowIt) in tool and equipment rental in Germany
  that are not listed yet, maintains competitors.md and creates one detail file per find.
  Use this skill when someone wants to find new competitors, update the competitor list or
  run a competitor update.
triggers:
  - "New competitors"
  - "Update competitors"
  - "Find competitors"
  - "Extend the competitor list"
---

# PATHS (fixed)

| Short name             | Path                                    |
| ---------------------- | --------------------------------------- |
| Overview               | `competitors/competitors.md`            |
| Detail per competitor  | `competitors/competitor-[name].md` (`[name]` = lowercase-hyphen) |

# STEPS

## 1. Read the overview
Does `competitors/competitors.md` exist? No → create it with this header:

```markdown
| Name | Found on | File |
|------|----------|------|
```

## 2. Extract existing names
Pull the list of competitors that are already listed. Watch for spelling variants (upper/lower case, space vs hyphen) — no duplicates caused by spelling alone.

## 3. Search pass
One WebSearch pass on tool and equipment rental in Germany. Search with German terms (e.g. "Werkzeug leihen", "Geräteverleih", "Werkzeug mieten Nachbarn"), because the market is German. Find up to **2 candidates** that are NOT listed yet.

No candidates found → go to step 6 and note that there. Do not create any files.

## 4. Start sub-agents
For each new candidate (max. 2, in parallel) start one sub-agent. Each sub-agent:
- does short research on exactly one candidate
- writes `competitors/competitor-[name].md` using the template below, in English
- no further recursion (a sub-agent does not start sub-agents itself)

## 5. Extend the overview
After the sub-agents return: add one row per new competitor to `competitors/competitors.md` — name, today's date (YYYY-MM-DD), link to the detail file.

## 6. Summary
Show what was added and what was skipped (already listed). If nothing was found, say so explicitly, do not leave it empty.

---

# RULES

- **Cap of 2 candidates per run** — time budget over completeness.
- **Sub-agents:** max. 2 in parallel, one per candidate, no further recursion.
- **No invented facts or URLs.** Without a verified source: give the search term instead of inventing a source.
- File names: lowercase-hyphen, no spaces.
- Write everything in English, including file content. Use the vocabulary from `AGENTS.md` (borrower, lender, neighbourhood, tool/equipment, inSUREed, Pic & Done, hyperlocal).

---

# TEMPLATE

Applies to `competitor-[name].md`:

```markdown
# {Competitor name}

## Short description
{2-4 sentences: what the company does}

## Similarities
{2-4 sentences: what is similar to LeihsDir}

## Differences from LeihsDir
{2-4 sentences: what is concretely different}

## Business model
{2-4 sentences: how the company makes money}
```
