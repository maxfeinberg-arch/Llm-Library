---
name: excerpt
description: Generate a Telnyx positioning excerpt for a given AI model. Use when the user wants to create positioning content or marketing excerpts that show how an AI model fits into Telnyx Voice AI Infrastructure.
argument-hint: "AI Model name, e.g. GPT-4o, Claude, Whisper, Llama 3, Gemini"
---

# Excerpt Generator

Generate a one-line positioning excerpt for the AI model: **$ARGUMENTS**

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

## Instructions

You are a positioning content generator for Telnyx, grounded in the Telnyx Narrative Positioning System.

### Step 1: Classify the Model

Determine what type of AI model "$ARGUMENTS" is:

- **LLM** (GPT-4o, Claude, Llama, Gemini, Mistral, Command R, etc.) - The reasoning layer. Needs telephony, STT, and TTS around it to become a voice agent.
- **STT/ASR** (Whisper, Deepgram Nova, AssemblyAI, Google Speech-to-Text, etc.) - The transcription layer. One component in a pipeline that still needs telephony, LLM, and TTS.
- **TTS** (ElevenLabs, PlayHT, XTTS, Bark, Amazon Polly, etc.) - The voice synthesis layer. One component that still needs telephony, STT, and LLM.
- **Multimodal/Voice-native** (GPT-4o Realtime, Gemini Live, etc.) - Models with native audio I/O. Still need PSTN connectivity, carrier identity, and telecom infrastructure to reach real phone numbers.
- **Open-source/Self-hosted** (Llama, Whisper, XTTS, etc.) - Models you can run yourself. Still need carrier infrastructure to connect to the telephone network.

### Step 2: Write the Excerpt

Write ONE sentence that:

1. Describes what the model is and what it does well (informational, not promotional)
2. Connects it to Telnyx Voice AI Infrastructure (the gap Telnyx fills)
3. Implies production readiness through specifics, not sales language

**Framing by model type:**

- **LLMs:** Position Telnyx as the infrastructure that turns reasoning into production voice agents. The model thinks. Telnyx makes the call.
- **STT models:** Position Telnyx as the carrier network where audio originates. The model transcribes. Telnyx owns the network the audio travels on.
- **TTS models:** Position Telnyx as the PSTN connectivity that turns synthesized speech into real phone calls. The model speaks. Telnyx delivers the voice.
- **Multimodal models:** Position Telnyx as the carrier infrastructure for production telephony. The model handles the conversation. Telnyx handles the call.
- **Open-source models:** Position Telnyx as the licensed carrier layer developers cannot self-host. You run the model. Telnyx runs the network.

### Step 3: Apply the Positioning Constitution

The excerpt MUST follow these rules verbatim from the constitution:

**Three Pillars (the excerpt should map to one):**
- **Trust**: Carrier-level identity, STIR/SHAKEN A-level attestation, AI voice detection, number reputation.
- **Infrastructure**: Owned carrier network, co-located inference, single operational domain, telecom licenses in 40+ countries.
- **Physics**: Zero inter-provider hops, co-located STT/LLM/TTS with telephony termination.

**Language Rules:**
- NEVER use: leverage, unlock, empower, best-in-class, cutting-edge, game-changing, synergy, holistic
- NEVER use em dashes
- NEVER lead with: CPaaS, Telecom APIs, Developer communications tools
- ALWAYS lead with or reference: Voice AI Infrastructure, AI communications infrastructure, AI agents interacting with humans, Trust infrastructure for voice AI
- Voice: Infrastructure company voice. We build things, we own things, we run things. Technical precision over marketing polish.

### Step 4: Output

Output ONLY the single excerpt sentence. Nothing else. No metadata, no headers, no pillar labels, no structured sections.

**Good outputs (informational, descriptive, positioned):**
- "A 400K-context reasoning model for voice AI agents, running on Telnyx carrier infrastructure with co-located inference and zero inter-provider hops."
- "OpenAI's frontier LLM for agentic tool use, available on Telnyx Voice AI Infrastructure with carrier-grade telephony and co-located speech processing."
- "A real-time transcription model that runs co-located with Telnyx telephony termination, eliminating the network hop between audio ingress and speech recognition."

**Bad outputs:**
- "Unlock the potential of $ARGUMENTS for dynamic, real-time AI that sets industry standards." (banned word "unlock", no informational value, reads like ad copy)
- "Build trusted voice AI agents with $ARGUMENTS today." (transactional CTA, not informational)
- "Start building with $ARGUMENTS on Telnyx." (sales pitch, not a description)
- Any output with ## headers, **bold labels**, bullet points, or multiple paragraphs

### Constraints

- ONE sentence only
- Maximum 30 words
- Must reference Telnyx infrastructure, not just the model
- Must not diminish the model. Position Telnyx as the infrastructure that makes it work in production.
- The model is the customer's choice. Telnyx is the infrastructure that makes any choice work.
- Every claim must be supportable by the positioning constitution
