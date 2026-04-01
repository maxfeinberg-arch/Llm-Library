---
name: excerpt
description: Generate a Telnyx positioning excerpt for a given AI model. Use when the user wants to create positioning content or marketing excerpts that show how an AI model fits into Telnyx Voice AI Infrastructure.
argument-hint: "AI Model name, e.g. GPT-4o, Claude, Whisper, Llama 3, Gemini"
---

# Excerpt Generator

Generate a one-line positioning excerpt for the AI model: **$ARGUMENTS**

## What is an excerpt?

An excerpt is a single sentence of positioning copy that appears directly beneath the model name (H1) on a Telnyx model page. The H1 is already the model name. The excerpt is the one line underneath it.

**Example page layout:**
```
[H1] GPT-3.5 Turbo-0125
[Excerpt] Build production voice AI agents with GPT-3.5 Turbo on Telnyx carrier infrastructure.
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

1. Names what the model does well (acknowledge its strength)
2. Connects it to Telnyx Voice AI Infrastructure (the gap Telnyx fills)
3. Implies production readiness (not a demo, not a toy)

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

**Good outputs:**
- "Run $ARGUMENTS on Telnyx Voice AI Infrastructure with co-located inference, carrier-grade telephony, and zero inter-provider hops."
- "Build trusted voice AI agents with $ARGUMENTS on the same carrier network where calls originate and terminate."
- "Connect $ARGUMENTS to the telephone network with Telnyx carrier infrastructure, A-level STIR/SHAKEN attestation, and co-located speech processing."

**Bad outputs:**
- "Unlock the potential of $ARGUMENTS for dynamic, real-time AI that sets industry standards." (uses banned word "unlock", no positioning substance, no infrastructure reference)
- Any output with ## headers, **bold labels**, bullet points, or multiple paragraphs

### Constraints

- ONE sentence only
- Maximum 30 words
- Must reference Telnyx infrastructure, not just the model
- Must not diminish the model. Position Telnyx as the infrastructure that makes it work in production.
- The model is the customer's choice. Telnyx is the infrastructure that makes any choice work.
- Every claim must be supportable by the positioning constitution
