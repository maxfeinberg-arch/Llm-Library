# The Three Pillars

Everything Telnyx publishes maps to one of these three. No exceptions.

## Pillar 1: Trust

AI agents are beginning to interact directly with humans - handling customer support, verifying identities, conducting transactions, operating contact centers. When an AI agent calls a human, both parties need to know who they're talking to.

The internet doesn't provide identity. The telephone network does. Telnyx operates that infrastructure and runs AI directly on it.

- Telnyx is a licensed carrier providing full A-level STIR/SHAKEN attestation - the highest level of identity verification in the US telephone network
- Application-layer voice AI platforms cannot provide carrier-level attestation; they inherit whatever their telephony provider gives them
- AI voice cloning makes spoofing trivially easy - without carrier-level attestation, an AI agent calling from a spoofed number is indistinguishable from a scam call
- AI-powered voice fraud losses estimated at $4B+ globally in 2025 (Juniper Research, 2024)
- Telnyx polices its network, ensuring numbers are not labeled bad
- Reputation visibility: reputation dashboard/API so you can see and manage your number reputation
- Branded Calling: caller identity displayed to the recipient
- AI voice detection: within four seconds, determine if a call is AI-generated or human
- Inbound: free spam detection
- SIM Card as identity layer

## Pillar 2: Infrastructure

Telnyx owns the carrier network, operates the switching infrastructure, holds direct interconnects with tier-1 carriers globally, and runs AI inference on the same network.

This is not a reseller model. Telnyx originates and terminates calls on infrastructure it owns. No other voice AI platform owns both the carrier network and the inference infrastructure.

- Co-located inference: STT, LLM routing, and TTS run in the same facilities where voice calls terminate
- Single operational domain: one SLA, one support escalation, one auth boundary
- Cross-layer debugging: Telnyx traces a single call from PSTN ingress through inference and back to PSTN egress. In a Frankenstack, no single vendor sees across layers. The customer becomes the debugger.
- Carrier-level fixes others can't touch: call routing, number porting, CNAM/caller ID, STIR/SHAKEN attestation, moving LRNs, TFN template and CIC changes, international routing quality. No voice AI startup has carrier-level access.
- Real-time production intervention: reroute calls mid-incident at the carrier level, failover to backup inference, adjust media paths. The customer touches nothing.
- AI-powered support flywheel: Telnyx uses its own voice AI infrastructure to run support. Automated diagnostics pull full call traces, identify root cause, and resolve before a human touches it.
- The same architecture that eliminates network hops also eliminates vendor blame. When the entire call path runs on one system, debugging becomes possible.
- Data sovereignty by design: voice data processed in-region without cross-border transfer
- Telecom licenses in 40+ countries - a time-based moat requiring multi-year regulatory processes per jurisdiction
- Direct IP connectivity for HD calling
- Multi-cloud infrastructure - up all the time
- Owns the actual IP network (plays into physics)
- VXCs - bypass the internet altogether for services
- Multi-site/Multi-POP per region
- Wireless Mobile Core deployed globally for local-breakout

## Pillar 3: Physics

Latency in multi-vendor voice AI pipelines is primarily a network problem, not a model problem.

- Each vendor boundary adds 30-80ms of network overhead from routing audio across the public internet between separate companies
- Speed of light in fiber: ~5ms per 1,000km. US-East to Sydney: ~150ms round-trip just for physics
- Retell AI's "industry-leading" benchmark of ~600ms reveals how constrained multi-vendor architectures are (retellai.com)
- Telnyx's co-located architecture eliminates inter-provider network hops entirely [BENCHMARK PENDING - contact engineering for current P50/P99 measurements]

**The narrative flow: Trust -> Infrastructure -> Physics.** Trust is the reason. Infrastructure is the strategy. Physics is the proof.
