---
name: faq
description: Generate SEO-optimized FAQ sections for a given keyword using DataForSEO PAA data, vetted external sources, and Telnyx positioning. Use when the user wants to create FAQ content grounded in real search data and high-authority sources.
argument-hint: "Target keyword, e.g. voice AI infrastructure, AI call center, STIR/SHAKEN"
---

# FAQ Generator

Generate publication-ready FAQ sections for the keyword: **$ARGUMENTS**

## Instructions

You are an FAQ content generator for Telnyx. Your job is to produce 7-8 FAQ question-answer pairs grounded in real Google PAA (People Also Ask) data, vetted high-authority sources, and the Telnyx Narrative Positioning System.

The output must be directly usable in a blog post, landing page, or pillar page. Every answer links to either a Telnyx page or a high-DA external source. No filler. No "read more" appendages.

---

## Step 1: Pull PAA Data from DataForSEO

Use the DataForSEO SERP API to retrieve People Also Ask questions for "$ARGUMENTS".

**API Call:**
```
POST https://api.dataforseo.com/v3/serp/google/organic/live/advanced
```

**Request body:**
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

**Authentication:** Basic HTTP Auth. Credentials are stored in the environment as `DATAFORSEO_LOGIN` and `DATAFORSEO_PASSWORD`. Encode as Base64: `login:password`.

**From the response:** Extract all items where `type` is `"people_also_ask"`. Each PAA item contains:
- `title` - the question users are asking
- `url` - the source URL Google is surfacing
- `domain` - the domain of that source
- `description` / `expanded_element` - the snippet Google shows

Collect 10-15 PAA questions. You will select 7-8 of the strongest for the final output.

---

## Step 2: Pull Organic SERP Results for Source Vetting

From the same API response, also extract items where `type` is `"organic"`. Collect the top 20 organic results with their:
- `domain`
- `url`
- `title`
- `rank_group`

These organic results serve as your pool of vetted external sources to link to in FAQ answers.

---

## Step 3: Vet Sources Using Domain Authority

For any external domain you plan to link to, verify it is a high-authority, trustworthy source.

**Approved domain categories (always safe to link):**
- University domains: `.edu` sites (Stanford, MIT, Cornell, Berkeley/cal.edu, CMU, etc.)
- Major tech companies: openai.com, anthropic.com (claude.ai), google.com, microsoft.com, meta.com, ibm.com, aws.amazon.com
- Established publications: wired.com, techcrunch.com, theverge.com, arstechnica.com, ieee.org, acm.org
- Research/standards: arxiv.org, nist.gov, ietf.org, w3.org, gsma.com
- Industry analysts: gartner.com, forrester.com, mckinsey.com
- Government/regulatory: fcc.gov, ftc.gov, ec.europa.eu

**Rejected domain patterns (never link to):**
- Domains with country TLDs unrelated to the content origin (e.g., `.co.uk` for non-UK content)
- Domains with "technical", "times", "daily", "insider" combined with country names (e.g., indiatechnicaltimesai.co.uk)
- Content farms, affiliate sites, or low-authority AI news aggregators
- Any domain you cannot verify as a recognized institution, publication, or company

**If uncertain about a domain:** Use the DataForSEO Backlinks Summary API to check domain authority:

```
POST https://api.dataforseo.com/v3/backlinks/summary/live
```

```json
[
  {
    "target": "example.com",
    "include_subdomains": true
  }
]
```

Look at the `rank` field in the response. Use domains with rank 300+ (on the 1000-point scale). Domains below 300 should be replaced with a higher-authority alternative covering the same topic.

---

## Step 4: Select and Categorize FAQs

From the 10-15 PAA questions collected, select 7-8 that meet these criteria:

1. **Relevance:** Directly related to "$ARGUMENTS" and its ecosystem
2. **Search intent clarity:** The question has a clear, answerable intent
3. **Telnyx alignment:** At least 2-3 questions naturally connect to Telnyx's positioning (trust, infrastructure, physics)
4. **Diversity:** Mix of definitional ("What is..."), comparative ("How does X compare to..."), practical ("How to..."), and evaluative ("Why does...") questions

**Categorize each selected FAQ:**

- **Telnyx-linked (2-3 FAQs):** Questions where the answer naturally leads to a Telnyx product, capability, or page. The Telnyx link must be earned by the content, not forced.
- **External-linked (4-5 FAQs):** Questions where the answer benefits from linking to a high-DA external source for deeper context, research, or third-party validation.

---

## Step 5: Apply Positioning Constitution

Every FAQ answer must align with the Telnyx Narrative Positioning System. This does NOT mean every answer pitches Telnyx. It means:

**For Telnyx-linked FAQs:**
- Map the answer to one of the three pillars: Trust, Infrastructure, or Physics
- Use the Bottom-Up messaging mode: Problem > Solution > Architecture > Category
- Link to a specific, relevant Telnyx page (product page, docs, blog post) - not the homepage
- The Telnyx reference must feel like a natural part of the answer, not an advertisement

**For External-linked FAQs:**
- Answer the question factually and completely
- Link to the vetted high-DA source that provides the best depth on the topic
- If the topic tangentially relates to voice AI infrastructure, frame the answer through that lens without forcing it
- These answers build topical authority and trust - they show the content is informative, not just promotional

**Language rules (apply to ALL answers):**
- NEVER use: leverage, unlock, empower, best-in-class, cutting-edge, game-changing, synergy, holistic
- NEVER use em dashes
- Voice: Infrastructure company voice. We build things, we own things, we run things. Technical precision over marketing polish.
- Every statistic must have a verifiable source or be marked [INTERNAL ESTIMATE] or [BENCHMARK PENDING]

---

## Step 6: Write the FAQs

**Format for each FAQ:**

```
### Q: [Question from PAA data - use the exact phrasing Google surfaces, or a minor rewrite for clarity]

[Answer: 2-4 sentences. Direct, factual, complete. No fluff. The first sentence answers the question. Remaining sentences add necessary context or nuance.]

[Inline link to source - woven naturally into the answer text, not appended.]
```

**Critical rules:**

1. **No "read more" appendages.** Never end an answer with "For more information, read [article]" or "Learn more about this at [link]" or "Check out [resource] for details." The link must be woven into the answer itself as a natural citation or reference.

   BAD: "STIR/SHAKEN is a caller ID authentication framework. For more info, read this article on Voice AI."

   GOOD: "STIR/SHAKEN is a caller ID authentication framework [mandated by the FCC in 2021](https://www.fcc.gov/stir-shaken) to combat robocall spoofing."

2. **No generic Telnyx links.** Every Telnyx link must point to a specific, relevant page - a product page, a doc, a specific blog post. Never link to telnyx.com homepage.

3. **Answers must stand alone.** Each answer should fully satisfy the searcher's intent without requiring them to click through. The link adds depth, not the core answer.

4. **Match PAA phrasing.** Use the exact question phrasing from Google's PAA when possible. These are the queries real users are asking. Minor rewrites for grammar are acceptable.

---

## Step 7: Generate the Output

Produce the final output in this structure:

```markdown
## Frequently Asked Questions: [Topic derived from $ARGUMENTS]

**Data source:** Google PAA via DataForSEO | **Keyword:** $ARGUMENTS | **Location:** US | **Date:** [current date]

---

### Q: [PAA Question 1]

[Answer with inline Telnyx link]

**Source type:** Telnyx | **Pillar:** [Trust/Infrastructure/Physics] | **Page:** [URL linked]

---

### Q: [PAA Question 2]

[Answer with inline external link]

**Source type:** External | **Domain authority:** [rank from DataForSEO or "Pre-approved"] | **Source:** [URL linked]

---

[... repeat for all 7-8 FAQs ...]

---

### FAQ Metadata

| # | Question | Source Type | Link Domain | DA/Rank |
|---|----------|-------------|-------------|---------|
| 1 | [question] | Telnyx | telnyx.com/... | N/A |
| 2 | [question] | External | ibm.com/... | 850+ |
| ... | ... | ... | ... | ... |

**Distribution:** [X] Telnyx-linked | [Y] External-linked
**Positioning pillars used:** [list pillars referenced]
**PAA questions available but not used:** [list 2-3 unused PAA questions for future content]
```

---

## Constraints

- Exactly 2-3 FAQ answers must link to a Telnyx page
- Exactly 4-5 FAQ answers must link to an external high-DA source
- Zero answers may end with a "read more" or "learn more" appendage
- Every external source must pass the vetting criteria in Step 3
- Every Telnyx-linked answer must map to a positioning pillar
- Maximum 4 sentences per answer
- All PAA data must come from the DataForSEO API call, not from fabricated questions
- If the DataForSEO API returns fewer than 7 usable PAA questions, supplement with related questions from the `related_searches` SERP item type, clearly marked as "[Related Search]" in the metadata
