# The Enemy: The Frankenstack

The Frankenstack is the prevailing architecture for voice AI: assembling 4-6 separate vendors to build a single voice AI pipeline.

A typical Frankenstack:

| Layer | Example Vendor | Function |
|---|---|---|
| Telephony | Twilio | PSTN connectivity, number provisioning |
| Speech-to-Text | Deepgram / AssemblyAI | Real-time transcription |
| LLM | OpenAI / Anthropic | Reasoning and response generation |
| Text-to-Speech | ElevenLabs / PlayHT | Voice synthesis |
| Orchestration | Vapi / Retell / custom | Glue logic connecting the above |
| Media Transport | LiveKit / custom WebRTC | Audio routing between components |

What goes wrong:

- **Latency compounds.** Each vendor boundary adds 30-80ms of network overhead. A 5-hop pipeline adds 150-400ms before any model runs.
- **Reliability degrades.** Five vendors at 99.9% uptime each = 99.5% compound availability = ~4.4 hours of downtime per month.
- **Debugging is impossible.** Five dashboards, five support teams, no end-to-end trace.
- **Costs stack.** Each vendor takes margin. Total cost: 2-4x what integrated infrastructure charges. [INTERNAL ESTIMATE]
- **Identity breaks.** STIR/SHAKEN attestation lives at the telephony layer. The STT/LLM/TTS vendors never see it.
- **Compliance fragments.** Data flows through five companies, five DPAs, five security postures.

The Telnyx alternative:

One infrastructure. Telephony, STT, LLM routing, TTS, and orchestration - all running on the same carrier network. One SLA. One vendor. One bill. Zero inter-provider network hops.
