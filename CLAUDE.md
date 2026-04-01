# LLM-Library

This repo contains Claude Code skills for generating Telnyx Voice AI Infrastructure positioning content. All content is grounded in the positioning constitution, split into focused files under `constitution/`.

## How Skills Work: Pipeline, Not Agentic

Both skills run as **sequential pipelines with human-in-the-loop checkpoints**. At each checkpoint, the user is presented with 4 options (via `AskUserQuestion` with preview fields) and can select one or choose "Other" to request regeneration with feedback. The skill does NOT proceed to the next step until the user makes a selection.

Steps within a stage run in parallel when they are independent (e.g., multiple API calls). Steps across stages run sequentially because each depends on the user's choice from the previous checkpoint.

## Skills

### `/excerpt <model name>`
Generates a single-sentence positioning excerpt for an AI model page on telnyx.com. Informational intent, not transactional. One sentence, max 30 words.

**Pipeline (1 checkpoint):**
1. **Research** (parallel: read constitution language file + web search model)
2. **Generate Excerpts** → **Checkpoint:** User picks from 4 excerpt sentences (each with a different angle), with previews. Regen available.

**Reads:** `constitution/language-and-messaging.md`

### `/faq <keyword>`
Generates 7-8 SEO-optimized FAQ sections using live Google PAA data from the DataForSEO API.

**Pipeline (4 checkpoints):**
1. **Pull Data** (parallel: 3 DataForSEO API calls) → **Checkpoint 1:** User reviews raw PAA questions, Telnyx pages, and organic sources. Confirms or adjusts.
2. **Select Questions** → **Checkpoint 2:** User picks from 4 curated question sets (different mixes of 7-8 from the pool), with previews
3. **Categorize & Assign Sources** → **Checkpoint 3:** User picks from 4 categorization variants (which FAQs get Telnyx vs external links), with previews
4. **Write FAQs** → **Checkpoint 4:** User picks from 4 complete FAQ outputs (different writing styles), with previews. Regen available.

**Reads:** `constitution/pillars.md`, `constitution/language-and-messaging.md`, `constitution/arguments.md`, `constitution/proof-layer.md`
**Requires:** DataForSEO credentials (`DATAFORSEO_LOGIN` / `DATAFORSEO_PASSWORD` env vars, or provided when prompted)

## Positioning Constitution

The constitution is split into focused files so skills only ingest what they need. Each file is verbatim from the source document. Do not summarize, paraphrase, or hallucinate positioning claims.

| File | Contents | Used by |
|------|----------|---------|
| `constitution/pillars.md` | Three Pillars: Trust, Infrastructure, Physics | excerpt, faq |
| `constitution/language-and-messaging.md` | Language rules, messaging hierarchy, two messaging modes | excerpt, faq |
| `constitution/arguments.md` | Five canonical arguments with evidence and rebuttals | faq |
| `constitution/proof-layer.md` | Proof points table (claims only Telnyx can make) | faq |
| `constitution/frankenstack.md` | The Frankenstack problem definition | reference |
| `constitution/narrative.md` | Category definition and core narrative | reference |
| `constitution/personas.md` | Persona table and 30-second sales scripts | reference |
| `constitution/competitive.md` | Competitive intelligence (ElevenLabs, Twilio, LiveKit, Vapi, Retell, Bland, Cloudflare) | reference |
| `constitution/strategy.md` | Journey maps, SEO/AEO strategy, content priorities, regional execution | reference |

**"reference"** means the file is not read by any skill automatically but is available for manual consultation.

## File Structure

```
CLAUDE.md                                # This file
01-positioning-constitution.md           # Full constitution (archive/reference)
constitution/
  pillars.md                             # Three Pillars
  language-and-messaging.md              # Language rules, hierarchy, modes
  arguments.md                           # Five canonical arguments
  proof-layer.md                         # Proof points table
  frankenstack.md                        # The Frankenstack problem
  narrative.md                           # Category & core narrative
  personas.md                            # Personas & sales scripts
  competitive.md                         # Competitive intelligence
  strategy.md                            # Journeys, SEO, content, regional
skills/
  excerpt/SKILL.md                       # Excerpt generator (2-checkpoint pipeline)
  faq/SKILL.md                           # FAQ generator (4-checkpoint pipeline)
```
