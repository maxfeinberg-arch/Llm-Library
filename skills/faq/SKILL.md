---
name: faq
description: Generate SEO-optimized FAQ sections for a given keyword using DataForSEO PAA data, vetted external sources, and Telnyx positioning. Use when the user wants to create FAQ content grounded in real search data and high-authority sources.
argument-hint: "Target keyword, e.g. voice AI infrastructure, AI call center, STIR/SHAKEN"
---

# FAQ Generator

Generate publication-ready FAQ sections for the keyword: **$ARGUMENTS**

This is a pipeline. Execute each step in order. Stop at each checkpoint and wait for the user's selection before proceeding.

Before starting, read these files for positioning rules:
1. `constitution/pillars.md` - The three pillars (Trust, Infrastructure, Physics)
2. `constitution/language-and-messaging.md` - Language rules, messaging hierarchy, messaging modes
3. `constitution/arguments.md` - Five canonical arguments (for framing FAQ answers)
4. `constitution/proof-layer.md` - Proof points (for sourcing claims)

---

## Step 1: Pull Data (run all 3 API calls in parallel)

**Authentication:** Basic HTTP Auth. Credentials: `DATAFORSEO_LOGIN` and `DATAFORSEO_PASSWORD` env vars. Encode as Base64: `login:password`. If credentials are not available, ask the user to provide them before proceeding.

### Call A: PAA + Organic Results

```
POST https://api.dataforseo.com/v3/serp/google/organic/live/advanced
```

```json
[
  {
    "keyword": "$ARGUMENTS",
    "location_code": 2840,
    "language_code": "en",
    "device": "desktop",
    "os": "windows",
    "depth": 10,
    "people_also_ask_click_depth": 3
  }
]
```

Extract:
- All `people_also_ask` items: `title`, `url`, `domain`, `expanded_element`
- All `organic` items: `domain`, `url`, `title`, `rank_group`

### Call B: Telnyx Page Discovery

```
POST https://api.dataforseo.com/v3/serp/google/organic/live/advanced
```

```json
[
  {
    "keyword": "site:telnyx.com $ARGUMENTS",
    "location_code": 2840,
    "language_code": "en",
    "device": "desktop",
    "os": "windows",
    "depth": 30
  }
]
```

Extract all organic results: `url`, `title`, `description`. This is the Telnyx link pool.

If zero results, run fallback:
```json
[
  {
    "keyword": "site:telnyx.com voice AI",
    "location_code": 2840,
    "language_code": "en",
    "device": "desktop",
    "os": "windows",
    "depth": 30
  }
]
```

### Call C: Supplementary PAA (if Call A returns fewer than 10 PAA questions)

Run a second PAA query with a broader keyword variation (e.g., "$ARGUMENTS capabilities", "$ARGUMENTS vs", "$ARGUMENTS use cases") to expand the question pool.

### Checkpoint 1: Review raw data

After all API calls complete, present the user with a summary:

- **PAA questions found:** list all questions with their source domains
- **Telnyx pages found:** list all discovered Telnyx URLs with titles
- **Organic sources found:** list top domains from organic results

Use `AskUserQuestion` to ask the user to confirm the data looks good:
- Option 1: "Data looks good, proceed"
- Option 2: "Run additional keyword variation" (user provides a new keyword to pull more PAA)
- Option 3: "Remove some questions" (user specifies which to exclude)
- Option 4: "Start over with different keyword"

**Do NOT proceed to Step 2 until the user confirms.**

---

## Step 2: Select Questions

From the PAA pool, curate 4 different sets of 7-8 questions. Each set should:

1. **Relevance:** Directly related to "$ARGUMENTS" and its ecosystem
2. **Search intent clarity:** Each question has a clear, answerable intent
3. **Telnyx alignment:** At least 2-3 questions naturally connect to Telnyx's positioning (trust, infrastructure, physics)
4. **Diversity:** Mix of definitional ("What is..."), comparative ("How does X compare to..."), practical ("How to..."), and evaluative ("Why does...") questions

Each of the 4 sets should emphasize a different mix (e.g., more technical, more comparative, more definitional, more production-focused).

### Checkpoint 2: Choose question set

Present the 4 question sets to the user using `AskUserQuestion` with the `preview` field showing the numbered list of questions in each set. The user picks one or selects "Other" to customize (add/remove specific questions).

**Do NOT proceed to Step 3 until the user selects a question set.**

---

## Step 3: Categorize & Assign Sources

Take the selected question set and produce 4 different categorization variants. Each variant assigns:

- **Telnyx-linked (2-3 FAQs):** Which questions link to a Telnyx page, which pillar they map to, and which specific Telnyx URL from the Step 1 discovery pool
- **External-linked (4-5 FAQs):** Which questions link to an external source, and which specific URL from the organic results or PAA expanded elements

Each variant should differ in which questions get Telnyx links vs external links, and which specific source URLs are assigned.

**Source vetting rules:**

Approved domains (always safe): `.edu` sites, openai.com, anthropic.com, google.com, microsoft.com, meta.com, ibm.com, aws.amazon.com, wired.com, techcrunch.com, theverge.com, arstechnica.com, ieee.org, acm.org, arxiv.org, nist.gov, ietf.org, w3.org, gsma.com, gartner.com, forrester.com, mckinsey.com, fcc.gov, ftc.gov, ec.europa.eu, forbes.com

Rejected patterns: country TLDs unrelated to content origin, "technical/times/daily/insider" + country names, content farms, affiliate sites, low-authority AI news aggregators.

If uncertain about a domain, check via DataForSEO Backlinks Summary API (`POST https://api.dataforseo.com/v3/backlinks/summary/live`). Use domains with `rank` 300+ only.

**Critical:** All URLs must come from the DataForSEO API results. Telnyx URLs from Call B. External URLs from Call A organic results or PAA expanded elements. Never fabricate or guess a URL.

### Checkpoint 3: Choose categorization

Present the 4 categorization variants to the user using `AskUserQuestion` with the `preview` field showing a table: question | source type | link URL | pillar (if Telnyx). The user picks one or selects "Other" to adjust assignments.

**Do NOT proceed to Step 4 until the user selects a categorization.**

---

## Step 4: Write FAQs

Using the selected questions, categorization, and source assignments, generate 4 complete FAQ outputs. Each output contains all 7-8 Q&A pairs but with different writing approaches:

- **Variant A:** Technical/developer voice, bottom-up framing
- **Variant B:** Concise/direct, minimal context
- **Variant C:** Explanatory, more context per answer
- **Variant D:** Mixed, technical for Telnyx-linked and accessible for external-linked

**Rules for all variants:**

1. **No "read more" appendages.** Never end with "For more information..." or "Learn more at..." The link must be woven into the answer as a natural citation.

   BAD: "STIR/SHAKEN is a framework. For more info, read this article on Voice AI."
   GOOD: "STIR/SHAKEN is a caller ID authentication framework [mandated by the FCC in 2021](https://www.fcc.gov/stir-shaken) to combat robocall spoofing."

2. **No fabricated links.** Every URL must come from the DataForSEO API results. Never guess or construct a URL.

3. **Answers stand alone.** Each answer fully satisfies the searcher's intent. The link adds depth, not the core answer.

4. **Match PAA phrasing.** Use the exact question phrasing from Google's PAA. Minor grammar rewrites only.

5. **Maximum 4 sentences per answer.**

6. **Language rules:** Never use banned words (leverage, unlock, empower, best-in-class, cutting-edge, game-changing, synergy, holistic). Never use em dashes. Infrastructure company voice. Every statistic must have a verifiable source or be marked [INTERNAL ESTIMATE] or [BENCHMARK PENDING].

**For Telnyx-linked FAQs:**
- Map to one of the three pillars: Trust, Infrastructure, or Physics
- Use Bottom-Up messaging: Problem > Solution > Architecture > Category
- Link ONLY to a Telnyx URL from Step 1 Call B results

**For External-linked FAQs:**
- Answer factually and completely
- Link ONLY to URLs from Step 1 Call A results
- Frame through voice AI infrastructure lens without forcing it

### Checkpoint 4: Choose final output

Present the 4 FAQ variants to the user using `AskUserQuestion` with the `preview` field showing the first 2-3 Q&A pairs of each variant (enough to show the tone/style). The user picks one or selects "Other" to request regeneration with specific feedback.

**If the user requests regeneration:** Generate 4 new variants incorporating their feedback. Repeat this checkpoint until the user selects one.

---

## Output

Once the user selects a variant, output the final FAQ in this format:

```markdown
## Frequently Asked Questions: [Topic derived from $ARGUMENTS]

**Data source:** Google PAA via DataForSEO | **Keyword:** $ARGUMENTS | **Location:** US | **Date:** [current date]

---

### Q: [Question]

[Answer with inline link]

**Source type:** Telnyx | **Pillar:** [Trust/Infrastructure/Physics] | **Page:** [URL]

---

### Q: [Question]

[Answer with inline link]

**Source type:** External | **Domain authority:** [rank or "Pre-approved"] | **Source:** [URL]

---

[... all 7-8 FAQs ...]

---

### FAQ Metadata

| # | Question | Source Type | Link Domain | DA/Rank |
|---|----------|-------------|-------------|---------|
| 1 | [question] | Telnyx | telnyx.com/... | N/A |
| 2 | [question] | External | domain.com/... | 850+ |

**Distribution:** [X] Telnyx-linked | [Y] External-linked
**Positioning pillars used:** [list]
**PAA questions available but not used:** [list 2-3 for future content]
```
