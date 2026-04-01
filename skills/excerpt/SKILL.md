---
name: excerpt
description: Generate a Telnyx positioning excerpt for a given AI model. Use when the user wants to create positioning content or marketing excerpts that show how an AI model fits into Telnyx Voice AI Infrastructure.
argument-hint: "AI Model name, e.g. GPT-4o, Claude, Whisper, Llama 3, Gemini"
---

# Excerpt Generator

Generate a one-line positioning excerpt for the AI model: **$ARGUMENTS**

This is a pipeline. Execute each step in order. Stop at each checkpoint and wait for the user's selection before proceeding.

---

## Search Intent: Informational

The page this excerpt lives on targets an informational keyword. The user is searching for "$ARGUMENTS" to learn what it is, how it works, or what it does. They are NOT looking to buy, compare pricing, or sign up for anything.

The excerpt must be informational first. It should describe what the model does and how it connects to voice AI infrastructure. It should NOT read like a sales pitch, a CTA, or a transactional landing page headline. The positioning is embedded in the framing, not in a hard sell.

**Informational tone:** "Here is what this model is and how it fits into production voice AI."
**NOT transactional tone:** "Start building with this model today." / "Sign up to use this model."

## What is an excerpt?

An excerpt is a single sentence of positioning copy that appears directly beneath the model name (H1) on a Telnyx model page. The H1 is already the model name. The excerpt is the one line underneath it.

**Example page layout:**
```
[H1] GPT-3.5 Turbo-0125
[Excerpt] A fast, cost-efficient LLM for voice AI agents, running on Telnyx carrier infrastructure with co-located inference.
[CTA buttons] START BUILDING | GET AVAILABLE MODELS
```

The excerpt is ONE sentence. Not a paragraph. Not a structured document. One line.

---

## Step 1: Research & Classify

**Actions (run in parallel):**
1. Read `constitution/pillars.md` and `constitution/language-and-messaging.md`
2. Research "$ARGUMENTS" using web search to understand what this model is, its capabilities, and its category

**Then classify** the model into one of these types:
- **LLM** - The reasoning layer. Needs telephony, STT, and TTS around it to become a voice agent.
- **STT/ASR** - The transcription layer. One component in a pipeline that still needs telephony, LLM, and TTS.
- **TTS** - The voice synthesis layer. One component that still needs telephony, STT, and LLM.
- **Multimodal/Voice-native** - Models with native audio I/O. Still need PSTN connectivity, carrier identity, and telecom infrastructure.
- **Open-source/Self-hosted** - Models you can run yourself. Still need carrier infrastructure to connect to the telephone network.

### Checkpoint 1: Choose the positioning angle

After classifying the model, present the user with 4 options using `AskUserQuestion`. Each option is a different positioning angle combining model type + pillar + framing direction. Use the `preview` field to show a one-line preview of what the excerpt would sound like for each angle.

**Example options (adapt to the specific model):**
- Option 1: Infrastructure pillar, co-location framing
- Option 2: Trust pillar, identity/attestation framing
- Option 3: Physics pillar, latency/network framing
- Option 4: Infrastructure pillar, single-stack framing

The user can also select "Other" to describe a custom angle.

**If the user requests regeneration:** Generate 4 new angles that are meaningfully different from the first set.

**Do NOT proceed to Step 2 until the user selects an angle.**

---

## Step 2: Generate Excerpts

Using the angle the user selected in Step 1, generate 4 distinct excerpt sentences. Each must:

1. Describe what the model is and what it does well (informational, not promotional)
2. Connect it to Telnyx Voice AI Infrastructure through the chosen angle
3. Imply production readiness through specifics, not sales language

**Framing reference by model type:**
- **LLMs:** The model thinks. Telnyx makes the call.
- **STT models:** The model transcribes. Telnyx owns the network the audio travels on.
- **TTS models:** The model speaks. Telnyx delivers the voice.
- **Multimodal models:** The model handles the conversation. Telnyx handles the call.
- **Open-source models:** You run the model. Telnyx runs the network.

**Language rules (from constitution):**
- NEVER use: leverage, unlock, empower, best-in-class, cutting-edge, game-changing, synergy, holistic
- NEVER use em dashes
- NEVER lead with: CPaaS, Telecom APIs, Developer communications tools
- ALWAYS lead with or reference: Voice AI Infrastructure, AI communications infrastructure, AI agents interacting with humans, Trust infrastructure for voice AI
- Voice: Infrastructure company voice. We build things, we own things, we run things. Technical precision over marketing polish.

**Constraints per excerpt:**
- ONE sentence only
- Maximum 30 words
- Must reference Telnyx infrastructure, not just the model
- Must not diminish the model
- Every claim must be supportable by the positioning constitution
- Informational tone, not transactional

### Checkpoint 2: Choose the excerpt

Present the 4 excerpts to the user using `AskUserQuestion` with the `preview` field showing each full sentence. The user picks one or selects "Other" to request regeneration with specific feedback.

**If the user requests regeneration:** Generate 4 new excerpts incorporating their feedback. Repeat this checkpoint until the user selects one.

---

## Output

Once the user selects an excerpt, output ONLY the final sentence. Nothing else. No metadata, no headers, no commentary. Just the one line of copy.
