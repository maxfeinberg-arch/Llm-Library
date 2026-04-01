# LLM-Library

This repo contains Claude Code skills for generating Telnyx Voice AI Infrastructure positioning content. All content is grounded in the positioning constitution, split into focused files under `constitution/`.

## Skills

### `/excerpt <model name>`
Generates a single-sentence positioning excerpt for an AI model page on telnyx.com. The excerpt sits directly below the model name (H1). One sentence, max 30 words. Informational intent, not transactional. No headers, no metadata, no structured output.

**Reads:** `constitution/pillars.md`, `constitution/language-and-messaging.md`

### `/faq <keyword>`
Generates 7-8 SEO-optimized FAQ sections using live Google PAA data from the DataForSEO API. Outputs publication-ready Q&A pairs with inline links to vetted sources.

- 2-3 FAQs link to real Telnyx pages (discovered via `site:telnyx.com` SERP query)
- 4-5 FAQs link to high-DA external sources (from organic SERP results)
- All URLs come from DataForSEO API results. Never fabricate or guess a URL.
- Requires DataForSEO credentials: `DATAFORSEO_LOGIN` and `DATAFORSEO_PASSWORD` env vars, or provide credentials directly when prompted.

**Reads:** `constitution/pillars.md`, `constitution/language-and-messaging.md`, `constitution/arguments.md`, `constitution/proof-layer.md`

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
  excerpt/SKILL.md                       # Excerpt generator skill
  faq/SKILL.md                           # FAQ generator skill
```
