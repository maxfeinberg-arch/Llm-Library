---
name: about
description: Generate a 350-400 character "About" paragraph for a given AI model on a Telnyx model page. Single paragraph, no links, no line breaks. Requires the model's excerpt to avoid repetition. Use when the user wants to create descriptive model content grounded in real research and Telnyx positioning.
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

## Step 1: Research (run in parallel)

### Action A: Read Constitution

Read `constitution/pillars.md` and `constitution/language-and-messaging.md` for voice guidelines, banned words, and positioning rules.

### Action B: Web Search for Model Context

Research "$ARGUMENTS" using web search to understand:
- What the model is and who built it
- Key capabilities and intended use cases
- Architecture details (parameter count, context window, modalities, etc.)
- Release date and versioning
- What differentiates it from prior versions or competitors

---

## Step 2: Get the Excerpt

Now that research is complete, ask the user for the model's excerpt. The excerpt is the one-sentence description that appears directly under the H1 on the model page. The About paragraph lives below it and must build on what the excerpt already says, not repeat it.

**How to get the excerpt:**
1. Check if the user already provided it earlier in the conversation
2. If not, check the `/excerpt` skill output history in this conversation
3. If neither is available, ask the user: "What is the current excerpt for [model name]? I need it so the About paragraph builds on it instead of repeating it."

**Do NOT proceed to Step 3 until you have the excerpt.**

Record the excerpt verbatim. You will reference it in Step 3 to ensure the About paragraph expands beyond it.

---

## Step 3: Generate About Paragraphs

Using the research from Step 1 and the excerpt from Step 2, generate 4 distinct "About" paragraphs. Each should take a different angle on the model.

### Content Requirements

1. **Character count:** 350-400 characters (including spaces). Count carefully. Under 350 or over 400 is a fail.
2. **Format:** One single paragraph. No line breaks. No paragraph breaks. No bullet points. No headers. Just one block of flowing text.
3. **No hyperlinks.** Do not include any links, URLs, or anchor text.
4. **Excerpt awareness:** The excerpt already introduces the model in one sentence. The About paragraph must NOT restate, rephrase, or echo the excerpt. Instead, it should assume the reader just read the excerpt and go deeper. If the excerpt says "optimized for instruction-following tasks with strong multilingual performance at efficient scale," the About paragraph should explain HOW it achieves that (architecture, training data, context window) rather than saying the same thing in more words.

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

[The selected 350-400 character about paragraph]

---

### Metadata

| Field | Value |
|-------|-------|
| **Character count** | [exact count] |
| **Excerpt used** | [the excerpt, verbatim] |
| **Data source** | Web search | [current date] |
| **Constitution files used** | pillars.md, language-and-messaging.md |
| **Variant selected** | [A/B/C/D] |
```
