---
name: about
description: Generate a 250-300 word "About" section for a given AI model on a Telnyx model page. Informational, multi-paragraph, with two verified hyperlinks. Use when the user wants to create descriptive model content grounded in real search data and Telnyx positioning.
argument-hint: "AI Model name, e.g. GPT-4o, Claude, Whisper, Llama 3, Gemini"
---

# About Section Generator

Generate a publication-ready "About" section for the AI model: **$ARGUMENTS**

This is a pipeline. Execute each step in order. Stop at each checkpoint and wait for the user's selection before proceeding.

Before starting, read these files for positioning rules:
1. `constitution/pillars.md` - The three pillars (Trust, Infrastructure, Physics)
2. `constitution/language-and-messaging.md` - Language rules, messaging hierarchy, messaging modes

---

## Search Intent: Informational

The page this about section lives on targets an informational keyword. The user searching "$ARGUMENTS" wants to understand what the model is, how it works, and what it does well. The about section educates. It does NOT sell.

The writing must be purely informational. It describes the model, its architecture, capabilities, and practical applications. It does NOT pitch Telnyx services, push a CTA, or frame the model through a commercial lens.

**Informational tone:** "Here is what this model is, how it works, and where it fits."
**NOT commercial tone:** "Deploy this model on Telnyx infrastructure today."

---

## Step 1: Research (run all actions in parallel)

### Action A: Read Constitution

Read `constitution/pillars.md` and `constitution/language-and-messaging.md` for voice guidelines, banned words, and positioning rules.

### Action B: Web Search for Model Context

Research "$ARGUMENTS" using web search to understand:
- What the model is and who built it
- Key capabilities and intended use cases
- Architecture details (parameter count, context window, modalities, etc.)
- Release date and versioning
- What differentiates it from prior versions or competitors

### Action C: DataForSEO Organic Search (External Article Discovery)

**Authentication:** Basic HTTP Auth. Credentials: `DATAFORSEO_LOGIN` and `DATAFORSEO_PASSWORD` env vars. Encode as Base64: `login:password`. If credentials are not available, ask the user to provide them before proceeding.

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
    "depth": 20
  }
]
```

Extract all `organic` items: `url`, `title`, `domain`, `description`, `rank_group`.

Filter for high-authority external articles about the model. Preferred domains: openai.com, anthropic.com, google.com, meta.com, microsoft.com, huggingface.co, arxiv.org, techcrunch.com, theverge.com, arstechnica.com, wired.com, ieee.org, venturebeat.com, towardsdatascience.com, forbes.com.

Rejected patterns: content farms, affiliate sites, low-authority AI aggregators, country TLD sites unrelated to content origin.

### Action D: DataForSEO Telnyx Page Discovery

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

Extract all organic results: `url`, `title`, `description`.

If zero results, run fallback queries in sequence until results are found:
1. `"site:telnyx.com AI models"`
2. `"site:telnyx.com voice AI"`
3. `"site:telnyx.com inference"`

Only accept Telnyx URLs that match one of these path patterns:
- `telnyx.com/developers/docs/...`
- `telnyx.com/resources/...`
- `telnyx.com/products/...`
- `telnyx.com/solutions/...`

If the discovered URLs do not match these patterns, search specifically:
```json
[
  {
    "keyword": "site:telnyx.com/developers OR site:telnyx.com/resources OR site:telnyx.com/products OR site:telnyx.com/solutions AI",
    "location_code": 2840,
    "language_code": "en",
    "device": "desktop",
    "os": "windows",
    "depth": 30
  }
]
```

---

### Checkpoint 1: Review Research Data

After all actions complete, present the user with a summary:

- **Model overview:** 2-3 sentence summary of what the model is
- **External articles found:** List the top 5 candidate external URLs with titles and domains
- **Telnyx pages found:** List all discovered Telnyx URLs (filtered to /developers/docs, /resources, /products, /solutions paths) with titles

Use `AskUserQuestion` to ask the user to confirm the data:
- Option 1: "Data looks good, proceed"
- Option 2: "Use different external article" (user specifies preference)
- Option 3: "Use different Telnyx page" (user specifies preference)
- Option 4: "Run additional search" (user provides a new query)

**Do NOT proceed to Step 2 until the user confirms.**

---

## Step 2: Verify Links

Before generating any content, verify that the top candidate URLs actually return a 200 status.

**For the external article:** Test the top 3 candidate URLs by fetching them. Use the first one that returns HTTP 200. If none return 200, go back to the organic results and test the next batch.

**For the Telnyx page:** Test all candidate Telnyx URLs by fetching them. Use the first one that returns HTTP 200 from the approved path patterns (/developers/docs, /resources, /products, /solutions). If none return 200, ask the user to provide a Telnyx URL manually.

**Both links MUST return HTTP 200 before proceeding.** Do not generate content with unverified links.

Record the two verified URLs for use in Step 3.

---

## Step 3: Generate About Sections

Using the research from Step 1 and the two verified URLs from Step 2, generate 4 distinct "About" sections. Each should take a different angle on the model.

### Content Requirements

1. **Word count:** 250-300 words. Count carefully. Under 250 or over 300 is a fail.
2. **Structure:** 3-4 paragraphs. Never one giant block of text. Use natural paragraph breaks that follow the logical flow of the content.
3. **Two hyperlinks (exactly):**
   - One to the verified external article about the model, woven naturally into the text as a citation or reference
   - One to the verified Telnyx page (/developers/docs, /resources, /products, /solutions), woven naturally into the text
4. **Informational tone:** Describe the model. Do not pitch Telnyx. The Telnyx link should appear where it naturally fits (e.g., mentioning that the model is available for inference, or linking to docs for integration details) without turning the section into an ad.
5. **No "read more" appendages.** Links must be inline citations, not trailing CTAs.

### Angle Differentiation

Each of the 4 variants should emphasize a different aspect:
- **Variant A:** Architecture and technical design (how the model works under the hood)
- **Variant B:** Capabilities and practical applications (what the model does well and where it fits)
- **Variant C:** Evolution and context (how this model advances the state of the art, what changed from previous versions)
- **Variant D:** Balanced overview (equal weight to architecture, capabilities, and ecosystem)

### Writing Rules

- **Voice:** Plain, precise, informational. Describe what the model does, not what it will do for the reader.
- **Banned words:** NEVER use: leverage, unlock, empower, best-in-class, cutting-edge, game-changing, synergy, holistic
- **No em dashes.**
- **Bottom-Up messaging** for the Telnyx-linked sentence: Problem > Solution > Architecture > Category. The model is available on infrastructure that reduces latency or simplifies deployment. State it plainly.
- **Every statistic must have a verifiable source** or be marked [BENCHMARK PENDING]. No unverified claims.
- **Do not diminish the model.** Describe its strengths honestly.
- **Do not mention Voice AI, phone calls, telephony, or voice agents** unless the model is specifically a speech/voice model. The reader may be here for any modality.
- **Paragraphs should flow logically:** e.g., what it is > how it works > what it does well > where to use it. Not rigid, but coherent.

### Link Integration Examples

**GOOD (external):** "GPT-4o processes text, images, and audio natively within a single architecture, a design [detailed in OpenAI's technical overview](https://openai.com/research/gpt-4o)."

**GOOD (Telnyx):** "Developers can access GPT-4o for inference through the [Telnyx LLM Router](https://telnyx.com/products/llm-router), which routes requests across providers from a single API."

**BAD:** "Learn more about GPT-4o on OpenAI's website. Check out Telnyx's products page for deployment options."

### Checkpoint 2: Choose the About Section

Present the 4 about sections to the user using `AskUserQuestion`. Put the full text of each variant in the `preview` field so the user can compare them side by side. Use labels like "Variant A: Architecture Focus", "Variant B: Capabilities Focus", etc.

The user picks one or selects "Other" to request regeneration with specific feedback.

**If the user requests regeneration:** Generate 4 new variants incorporating their feedback. Re-verify links if the user requests different URLs. Repeat this checkpoint until the user selects one.

---

## Output

Once the user selects a variant, output the final about section in this format:

```markdown
## About [Model Name]

[The selected 250-300 word about section with both inline hyperlinks]

---

### Metadata

| Field | Value |
|-------|-------|
| **Word count** | [exact count] |
| **External link** | [URL] — [domain] |
| **Telnyx link** | [URL] — [path pattern] |
| **External link status** | 200 OK |
| **Telnyx link status** | 200 OK |
| **Data source** | DataForSEO Organic | Google | [current date] |
| **Constitution files used** | pillars.md, language-and-messaging.md |
| **Variant selected** | [A/B/C/D] |
```
