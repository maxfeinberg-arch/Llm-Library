# Personas & Sales Scripts

## Personas

| Persona | Problem | Message |
|---|---|---|
| CEO / Founder | Voice AI infrastructure layer is being defined now; late entrants become commodity players | Build on the infrastructure that defines the category, not a platform that sits on top of it |
| CFO | Paying multiple vendors with compounding margins and compound downtime risk | Integrated infrastructure reduces cost and operational risk - one vendor, one bill, one SLA |
| VP Product | Engineering team spends more time integrating vendors than building product | One infrastructure, one API - time-to-production drops from months to weeks |
| CISO | Every vendor in the voice AI stack is an attack surface; voice data with PII traverses multiple third-party networks | One data boundary, one security posture, carrier-level identity verification, in-region data processing |
| General Counsel | AI agent makes regulated calls through a stack that can't be fully audited; data flows through 5 companies with different compliance postures | One regulated carrier environment, one DPA, built-in STIR/SHAKEN, telecom regulatory standing in 20+ countries |
| VP Contact Center | Voice downtime costs $5,600-$9,000/min (Gartner, large enterprise IT); fragmented infrastructure means fragmented reliability | Single-stack infrastructure - telephony, speech, and AI under one operational domain with one SLA |
| VP Customer Experience | Customers perceive AI agents with high latency as robotic; poor audio quality from multi-hop architectures damages brand | Co-located inference eliminates inter-provider hops; customers hear the difference |
| Developer / VP Eng | Multi-vendor pipeline = 4 network hops, 600ms+ latency, 4 support tickets when something breaks | Entire pipeline on one carrier network - zero inter-provider hops, one API, first call in 5 minutes |

---

## Per-Persona Sales Scripts (30 Seconds Each)

### The Killer Question (use to open any support/reliability conversation)

Ask the prospect:

> "When your voice AI agent goes down at 2am, who actually fixes the call?"

Pause. Let them think. In a Frankenstack the answer becomes obvious:
- Telephony vendor says it's the STT provider
- STT provider says it's the LLM
- LLM provider says it's the TTS
- Orchestration layer says it's telephony

The customer becomes the debugger.

Then land: "With Telnyx, you call one team. Because the entire call path runs on one system."

This turns support from "we have great support" into "your architecture determines whether support is even possible."

---

### Developer / VP Engineering

"Your voice AI pipeline probably chains together Twilio for telephony, Deepgram for STT, OpenAI for the LLM, and ElevenLabs for TTS. Four providers, four network hops, 600ms+ latency, and when something breaks you've got four support tickets open.

Telnyx runs the entire pipeline - telephony, speech recognition, language model routing, and speech synthesis - on the same carrier network. Zero inter-provider hops. One API. Here's the quickstart - first call in 5 minutes."

### CISO

"Your AI voice agent processes customer conversations through 4-5 separate vendors. Each vendor is a data boundary. Each boundary is an attack surface. Voice data containing PII, financial information, and health data traverses multiple third-party networks - each with separate security postures, separate DPAs, and separate breach risks.

Telnyx processes voice AI on carrier infrastructure we own. One data boundary. One security posture. Carrier-level STIR/SHAKEN attestation for identity verification. Data stays in-region. One SOC 2 audit, not five."

### CFO

"You're paying 5 vendors to run voice AI: telephony, speech-to-text, LLM, text-to-speech, and an orchestration layer to glue them together. Each vendor takes margin. Compound that and you're paying 2-4x what integrated infrastructure costs. [INTERNAL ESTIMATE]

Then add risk: enterprise IT downtime costs $5,600-$9,000 per minute (Gartner, large enterprise). Your compound availability across 5 vendors is 99.5%, not 99.9%. Telnyx consolidates the stack: one vendor, one bill, one SLA covering the end-to-end pipeline."

### VP Contact Center Operations

"Your contact center handles tens of thousands of calls a day. AI agents can handle 60%+ of them - if the infrastructure is reliable. On a multi-vendor voice AI stack, you're looking at 4+ hours of monthly downtime from compound vendor reliability.

Telnyx runs the entire voice AI pipeline on the same carrier network your calls traverse. One infrastructure. Your AI agents sound natural and don't drop calls because audio isn't bouncing between five different data centers."

### VP Product

"Your engineering team is spending more time integrating voice AI vendors than building product. The Frankenstack - Twilio + Deepgram + OpenAI + ElevenLabs + custom orchestration - takes 3-6 months to get to production and breaks every time a vendor pushes an API change. [INTERNAL ESTIMATE]

Telnyx is one infrastructure with one API. Telephony, STT, LLM routing, TTS - all integrated. Your team goes from integration plumbing to product development. Time-to-production drops from months to weeks."

### CEO / Founder

"Voice AI is becoming the primary interface between companies and customers. The infrastructure that voice AI runs on will be as important as cloud infrastructure was for web applications.

Right now, most companies are building voice AI on stitched-together vendor stacks. That's like building a web company on five different hosting providers in 2008. Telnyx is the infrastructure layer - carrier network, AI inference, and orchestration all in one. The companies that build on infrastructure win. The companies that build on application stacks get squeezed."

### General Counsel / VP Legal

"Your AI agent is making regulated phone calls - recorded, transcribed, potentially subject to consumer protection, AI disclosure, and wiretapping laws across multiple jurisdictions. The voice data flows through 4-5 separate companies, each with different compliance postures. Can you audit that? Can you defend it in court?

Telnyx operates licensed carrier infrastructure. Your AI calls, recordings, and transcriptions stay within one regulated environment. One DPA. One compliance framework. One entity to audit. Built-in STIR/SHAKEN attestation, data locality by region, and telecom regulatory standing in 20+ countries."

### VP Customer Experience

"Your customers don't care how many vendors power your AI agent. They care that it sounds natural, responds instantly, and doesn't drop their call.

Multi-vendor voice AI stacks average 600ms+ response latency - that's a noticeable pause in every exchange. Telnyx's co-located architecture eliminates inter-provider network hops entirely. Your customers hear the difference."
