---
name: about
description: Generate a 350-400 character "About" paragraph for a given AI model on a Telnyx model page. Single paragraph with one external hyperlink. Requires the model's excerpt to avoid repetition. Use when the user wants to create descriptive model content grounded in real research and Telnyx positioning.
argument-hint: "AI Model name, e.g. GPT-4o, Claude, Whisper, Llama 3, Gemini"
---

# About Section Generator

Generate a publication-ready "About" paragraph for the AI model: **$ARGUMENTS**

This is a pipeline. Execute each step in order. Stop at the checkpoint and wait for the user's selection before proceeding.

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

---

## Step 2: Verify External Link

After research completes, verify that the top candidate external URLs actually return a 200 status.

Test the top 3 candidate URLs by fetching them. Use the first one that returns HTTP 200. If none return 200, go back to the organic results and test the next batch.

**The external link MUST return HTTP 200 before proceeding.** Do not generate content with an unverified link.

Record the verified URL for use in Step 4.

---

## Step 3: Get the Excerpt

Now that research and the link are locked in, ask the user for the model's excerpt. The excerpt is the one-sentence description that appears directly under the H1 on the model page. The About paragraph lives below it and must build on what the excerpt already says, not repeat it.

**How to get the excerpt:**
1. Check if the user already provided it earlier in the conversation
2. If not, check the `/excerpt` skill output history in this conversation
3. If neither is available, ask the user: "What is the current excerpt for [model name]? I need it so the About paragraph builds on it instead of repeating it."

**Do NOT proceed to Step 4 until you have the excerpt.**

Record the excerpt verbatim. You will reference it in Step 4 to ensure the About paragraph expands beyond it.

---

## Step 4: Generate About Paragraphs

Using the research from Step 1, the verified external URL from Step 2, and the excerpt from Step 3, generate 4 distinct "About" paragraphs. Each should take a different angle on the model.

### Content Requirements

1. **Character count:** 350-400 characters (including spaces, excluding the hyperlink URL). Count carefully. Under 350 or over 400 is a fail.
2. **Format:** One single paragraph. No line breaks. No paragraph breaks. No bullet points. No headers. Just one block of flowing text.
3. **One external hyperlink (exactly one).** Link to the verified external article about the model, woven naturally into the text as an inline citation. Not a trailing "read more" or "learn more" appendage.
4. **Excerpt awareness:** The excerpt already introduces the model in one sentence. The About paragraph must NOT restate, rephrase, or echo the excerpt. Instead, it should assume the reader just read the excerpt and go deeper. If the excerpt says "optimized for instruction-following tasks with strong multilingual performance at efficient scale," the About paragraph should explain HOW it achieves that (architecture, training data, context window) rather than saying the same thing in more words.

### Link Integration

The hyperlink must be woven into the sentence as a natural citation, not appended at the end.

**GOOD:** "The model uses grouped-query attention and was pretrained on 15 trillion tokens, as [detailed in Meta's technical overview](https://ai.meta.com/blog/meta-llama-3-1/)."

**BAD:** "The model uses grouped-query attention. Learn more on Meta's blog."

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
- **Every statistic must have a verifiable source** or be marked [BENCHMARK PENDING]. No unverified claims.
- **Do not diminish the model.** Describe its strengths honestly.
- **Do not mention Voice AI, phone calls, telephony, or voice agents** unless the model is specifically a speech/voice model. The reader may be here for any modality.
- **Do not mention Telnyx.** The about paragraph is purely about the model itself.

### Checkpoint: Choose the About Paragraph

Present the 4 about paragraphs to the user using `AskUserQuestion`. Put the full text of each variant in the `preview` field so the user can compare them side by side. Use labels like "Variant A: Architecture Focus", "Variant B: Capabilities Focus", etc.

The user picks one or selects "Other" to request regeneration with specific feedback.

**If the user requests regeneration:** Generate 4 new variants incorporating their feedback. Repeat this checkpoint until the user selects one.

---

## Output

Once the user selects a variant, output the final about paragraph in this format:

```markdown
## About [Model Name]

[The selected 350-400 character about paragraph with inline hyperlink]

---

### Metadata

| Field | Value |
|-------|-------|
| **Character count** | [exact count] |
| **Excerpt used** | [the excerpt, verbatim] |
| **External link** | [URL] — [domain] |
| **External link status** | 200 OK |
| **Data source** | DataForSEO Organic | Web search | [current date] |
| **Constitution files used** | pillars.md, language-and-messaging.md |
| **Variant selected** | [A/B/C/D] |
```
