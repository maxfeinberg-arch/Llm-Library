---
name: excerpt
description: Generate an informational excerpt for a given AI model on a Telnyx model page. Use when the user wants to create a one-line description of what an AI model is and what it does well.
argument-hint: "AI Model name, e.g. GPT-4o, Claude, Whisper, Llama 3, Gemini"
---

# Excerpt Generator

Generate a one-line informational excerpt for the AI model: **$ARGUMENTS**

This is a pipeline. Execute each step in order. Stop at each checkpoint and wait for the user's selection before proceeding.

---

## Search Intent: Informational

The page this excerpt lives on targets an informational keyword. The user is searching for "$ARGUMENTS" to learn what it is, how it works, or what it does. They are NOT looking to buy, compare pricing, or sign up for anything.

The excerpt must be purely informational. It should describe what the model is and what it does well. It should NOT read like a sales pitch, a CTA, or a product page headline. No commercial framing at all.

**Informational tone:** "Here is what this model is and what it's good at."
**NOT commercial tone:** "Start building with this model today." / "Run this model on Telnyx infrastructure." / "Built for voice agents on carrier networks."

## What is an excerpt?

An excerpt is a single sentence that appears directly beneath the model name (H1) on a Telnyx model page. The H1 is already the model name. The excerpt is the one line underneath it.

**Example page layout:**
```
[H1] Claude Opus 4.6
[Excerpt] Anthropic's most capable model to date, built for complex reasoning, coding, and agentic workflows.
[CTA buttons] EXPLORE MODEL | VIEW DOCUMENTATION
```

**Reference examples (match this tone):**
- "GPT-5.3 brings stronger reasoning, richer answers, and better handling of context, making it relevant for both general users and developers."
- "GPT-5.3 is designed to improve everyday interactions with faster responses and more useful output."
- "Claude Opus 4.6 is Anthropic's most capable model to date, built for complex reasoning, coding, and agentic workflows."
- "Claude Opus 4.6 improves planning, tool use, and long-task reliability, making it useful for advanced workflows across coding and enterprise work."
- "Claude Opus 4.6 is designed to handle longer, more complex tasks with greater precision and less hand-holding."

The excerpt is ONE sentence. Not a paragraph. Not a structured document. One line.

---

## Step 1: Research

**Actions (run in parallel):**
1. Read `constitution/language-and-messaging.md` (for banned words and voice guidelines only)
2. Research "$ARGUMENTS" using web search to understand what this model is, its capabilities, its strengths, and its intended use cases

---

## Step 2: Generate Excerpts

Using the research from Step 1, generate 4 distinct excerpt sentences. Each should take a different angle on the model (e.g., primary strength, target use case, differentiator, design philosophy). Each must:

1. Describe what the model is and what it does well
2. Be informational and factual, not promotional or commercial
3. Sound like something you'd read in a neutral product description or tech article

**What the excerpt should do:**
- Lead with the model itself: what it is, who made it, what it's built for
- Describe capability, design intent, or practical value
- Be specific enough to be useful, general enough to apply across use cases

**What the excerpt must NOT do:**
- Mention Voice AI, phone calls, telephony, or voice agents (the user may be here for TTS, STT, or other non-voice-call uses)
- Mention Telnyx infrastructure, co-location, or carrier networks
- Sound like ad copy, a sales pitch, or a product landing page
- Use vague superlatives or marketing fluff
- Frame the model through any specific industry lens (telco, carrier, infrastructure, voice AI)

**Language rules (from constitution):**
- NEVER use: leverage, unlock, empower, best-in-class, cutting-edge, game-changing, synergy, holistic
- NEVER use em dashes
- Voice: Plain, precise, informational. Describe what the model does, not what it will do for you.

**Constraints per excerpt:**
- ONE sentence only
- Maximum 30 words
- Must not diminish the model
- Informational tone, not transactional or commercial
- Should read like the reference examples above
- Must be useful to any reader regardless of industry

### Checkpoint 2: Choose the excerpt

Present the 4 excerpts to the user using `AskUserQuestion`. Put the full excerpt sentence in the `description` field so the user can read all 4 without clicking into each one. Use a short label like "Excerpt 1", "Excerpt 2", etc. Do NOT use the `preview` field. The user picks one or selects "Other" to request regeneration with specific feedback.

**If the user requests regeneration:** Generate 4 new excerpts incorporating their feedback. Repeat this checkpoint until the user selects one.

---

## Output

**The excerpt describes the model. It does not describe the platform it's hosted on.**

Once the user selects an excerpt, output ONLY the final sentence. Nothing else. No metadata, no headers, no commentary. Just the one line of copy.
