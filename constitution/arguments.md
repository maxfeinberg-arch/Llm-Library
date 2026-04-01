# Five Canonical Arguments

### Argument 1: Voice AI latency is primarily a network problem

**Claim:** In multi-vendor voice AI stacks, the majority of non-inference latency comes from network hops between providers - not from model inference time.

**Evidence:** Typical pipeline: Audio -> STT provider (50-150ms inference + 30-80ms network) -> LLM provider (200-500ms inference + 30-80ms network) -> TTS provider (50-200ms inference + 30-80ms network) -> telephony provider (30-80ms network). Network overhead alone: 120-320ms. Retell AI's benchmark of ~600ms is considered "industry-leading" - revealing how broken multi-vendor architectures are.

**Counter/Rebuttal:** "We've optimized our pipeline to under 500ms." -> On a demo. In production, add variable network conditions, geographic distance to each provider, cold starts, queue times under load. P99 is what matters, not P50 on a demo.

**Telnyx proof:** Co-located inference with telephony termination. Zero inter-provider hops. [BENCHMARK PENDING for specific latency numbers]

### Argument 2: Reliability requires infrastructure ownership

**Claim:** Every vendor boundary is a failure domain. More vendors = more failure points = lower compound reliability.

**Evidence:** A 5-vendor stack where each delivers 99.9% uptime yields 99.5% compound availability - ~4.4 hours of downtime per month vs. ~43 minutes for single-vendor. Enterprise IT downtime costs $5,600-$9,000/minute for large enterprises (Gartner, 2024 - general enterprise IT, not voice-AI-specific). Each boundary also introduces separate auth, billing, support, SLAs, and incident response.

**Counter/Rebuttal:** "We use redundancy across providers." -> Redundancy across providers means maintaining parallel integrations, doubling costs, and managing failover logic that itself becomes a failure point. You're building infrastructure to compensate for not having infrastructure.

**Telnyx proof:** Single-stack: one SLA, one support escalation, one billing relationship. Telephony, speech, and inference all under one operational domain.

### Argument 3: Identity and trust require carrier infrastructure

**Claim:** When an AI agent calls a human, both parties need verified identity. Application-layer identity doesn't survive the PSTN boundary. The receiving carrier evaluates STIR/SHAKEN attestation from the originating carrier - not your app's auth token.

**Evidence:** FCC mandated STIR/SHAKEN for all US carriers (June 2021). Robocall complaints exceeded 2.4M annually to the FTC through 2024. AI voice cloning can replicate a voice from 3 seconds of audio. Without carrier-level attestation, an AI agent is indistinguishable from a scam call to the receiving network.

**Counter/Rebuttal:** "We handle identity in our application layer." -> Application-layer identity is invisible to the telephone network. If your telephony provider gives you B or C attestation, your calls get flagged or blocked regardless of your app's security.

**Telnyx proof:** Licensed carrier with A-level STIR/SHAKEN attestation. Calls signed at the carrier layer, not passed through a third party.

### Argument 4: Multi-vendor stacks explode cost and complexity

**Claim:** Frankenstacks compound vendor margins and operational complexity. Each vendor takes 20-40% margin; a 5-vendor stack compounds these. [INTERNAL ESTIMATE]

**Evidence:** Frankenstack cost: telephony per-minute + STT per-minute + LLM per-token + TTS per-character + orchestration platform fee. Integration time: 3-6 months to production for multi-vendor voice AI vs. 2-4 weeks for single-infrastructure. [INTERNAL ESTIMATE based on typical enterprise onboarding]

**Counter/Rebuttal:** "We pick best-of-breed for each layer." -> You can. And you'll spend 6 months integrating them, hit 800ms+ round-trip latency, and manage 5 separate vendor relationships, billing systems, and API changelogs. The model is 20% of the problem. The pipe is 80%.

**Telnyx proof:** One infrastructure, one API, one bill. Telephony, STT, LLM routing, TTS - all integrated.

### Argument 5: AI agents need real-world telecom connectivity

**Claim:** AI agents that can't reach humans on phone numbers and messaging channels are demos. Production agents need PSTN connectivity, SMS/MMS, and global number provisioning.

**Evidence:** 75% of consumers still prefer phone calls for complex support issues (Salesforce State of Service, 2024). Enterprise contact centers handle 60%+ of interactions via voice. The highest-value AI use cases - replacing human agents in customer service, healthcare, financial services - are voice-first.

**Counter/Rebuttal:** "Our agents work over chat/web." -> Chat and web cover a fraction of customer interaction surface area. The moment your AI needs to call a customer, receive an inbound call, send an SMS, or verify identity via phone - you need telecom infrastructure.

**Telnyx proof:** Voice, SMS, MMS, WhatsApp, number provisioning, verification, and WebRTC - all from the same carrier infrastructure that runs the AI pipeline.
