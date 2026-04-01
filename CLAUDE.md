# LLM-Library

This repo contains Claude Code skills for generating Telnyx Voice AI Infrastructure positioning content. All content is grounded in the positioning constitution at `01-positioning-constitution.md`.

## Skills

### `/excerpt <model name>`
Generates a single-sentence positioning excerpt for an AI model page on telnyx.com. The excerpt sits directly below the model name (H1). One sentence, max 30 words. No headers, no metadata, no structured output.

### `/faq <keyword>`
Generates 7-8 SEO-optimized FAQ sections using live Google PAA data from the DataForSEO API. Outputs publication-ready Q&A pairs with inline links to vetted sources.

- 2-3 FAQs link to real Telnyx pages (discovered via `site:telnyx.com` SERP query)
- 4-5 FAQs link to high-DA external sources (from organic SERP results)
- All URLs come from DataForSEO API results. Never fabricate or guess a URL.
- Requires DataForSEO credentials: `DATAFORSEO_LOGIN` and `DATAFORSEO_PASSWORD` env vars, or provide credentials directly when prompted.

## Positioning Constitution

`01-positioning-constitution.md` is the single source of truth for all content. Key rules:

- **Three Pillars:** Trust, Infrastructure, Physics. Every claim maps to one.
- **Narrative Flow:** Trust > Infrastructure > Physics. Trust is the reason. Infrastructure is the strategy. Physics is the proof.
- **Messaging Hierarchy:** Category > Core value > Platform proof > Product proof.
- **Banned words:** leverage, unlock, empower, best-in-class, cutting-edge, game-changing, synergy, holistic
- **No em dashes.**
- **Always lead with:** Voice AI Infrastructure, AI communications infrastructure, AI agents interacting with humans, Trust infrastructure for voice AI
- **Never lead with:** CPaaS, Telecom APIs, Developer communications tools
- **Voice:** Infrastructure company voice. We build things, we own things, we run things. Technical precision over marketing polish.
- **Numbers discipline:** Every statistic must have a verifiable source or be marked [INTERNAL ESTIMATE] or [BENCHMARK PENDING].

All references to the constitution in skill outputs must be verbatim. No summarizing, paraphrasing, or hallucinating positioning claims.

## File Structure

```
CLAUDE.md                          # This file
01-positioning-constitution.md     # Positioning source of truth
skills/
  excerpt/SKILL.md                 # Excerpt generator skill
  faq/SKILL.md                    # FAQ generator skill
```
