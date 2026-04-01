# Competitive Intelligence

## Tier 1: Dominant Threats (Fight for Market Definition)

### ElevenLabs

| Dimension | Assessment |
|---|---|
| Position | $11B valuation (Feb 2026, Series D, $500M raised). Leading voice synthesis company. Expanding into full conversational AI with "ElevenAgents." Partners: Deloitte, Revolut, Deutsche Telekom, Klarna, Liberty Global, Cisco. |
| Capabilities | Sub-100ms TTS latency (component only). 32+ languages. Conversational AI with voice + chat. Voice cloning. "Bring your own LLM." RAG integration. |
| Recent moves | ElevenLabs for Government (Feb 2026). Deutsche Telekom partnership for customer service across Europe (Jan 2026). Klarna deployment reducing resolution time by 10x. Scribe v2 transcription model. Vertically integrating from TTS -> full conversational AI platform. |
| Weakness | No telephony infrastructure. Cannot originate or terminate PSTN calls. No STIR/SHAKEN. No number provisioning. No SMS/MMS. No carrier licenses. "Sub-100ms" is component latency - end-to-end pipeline latency including telephony is much higher because they rely on third-party carriers. |
| Attack angle | "ElevenLabs makes the voice. Telnyx makes the call." Position as infrastructure ElevenLabs runs on. Simultaneously offer complete alternative pipeline (Telnyx TTS + STT + LLM Router) that eliminates the need for ElevenLabs entirely. Win-win: either they're a customer or they're displaced. |

### Twilio

| Dimension | Assessment |
|---|---|
| Position | ~$4.2B revenue (FY2024). Dominant CPaaS. ~300K customer accounts. Owns carrier infrastructure. Launching AI aggressively: ConversationRelay, AI Assistants. |
| Capabilities | ConversationRelay: connects Twilio voice calls to external LLM providers. Voice Intelligence: call transcription/analysis. AI Assistants: pre-built AI agents. They have telephony + are adding AI. |
| Recent moves | AI Assistants GA. ConversationRelay for real-time LLM-powered voice. Heavy AI narrative investment while core comms revenue is mature. |
| Weakness | Middleware architecture. AI features connect to external LLM/TTS providers - they're building a better Frankenstack, not eliminating it. No proprietary inference infrastructure. AI runs in AWS, not co-located with telephony. Per-unit pricing makes them expensive at scale. |
| Attack angle | "Twilio adds AI to telecom. Telnyx runs AI and telecom on the same infrastructure." Target installed base with: lower cost, lower latency (co-located inference), genuinely integrated architecture vs. bolt-on approach. Displacement content: "Migrate from Twilio to Telnyx Voice AI Infrastructure." |

### LiveKit

| Dimension | Assessment |
|---|---|
| Position | Open-source real-time communication framework. WebRTC infrastructure + AI Agents SDK. Growing rapidly in voice AI developer community. Backed by significant funding. Partnering with Together AI for GPU co-location. |
| Capabilities | WebRTC SFU (selective forwarding unit). AI Agents SDK for building voice AI agents. Telephony bridge via SIP (requires external carrier). Open-source core with cloud offering. Real-time audio/video transport. Growing ecosystem of plugins and integrations. |
| Weakness | No telephony infrastructure. No PSTN connectivity without an external carrier. No carrier licenses. No STIR/SHAKEN. No number provisioning. GPU co-location with Together AI improves inference latency but doesn't solve the telephony gap: calls still traverse LiveKit WebRTC -> SIP bridge -> external carrier -> PSTN. The carrier boundary remains. |
| Attack angle | "LiveKit moves GPUs closer. We run inference in the same rack as the telephony switch we own. They still need a carrier for every call. We are the carrier." Target developers already using LiveKit who hit the telephony wall. Content: architecture comparison showing full call path (LiveKit + carrier vs Telnyx end-to-end), "Why Your LiveKit Voice Agent Still Needs a Carrier," migration guides. Displacement queries: "livekit telephony," "livekit PSTN," "livekit vs telnyx." |

## Tier 2: Displacement Targets (Steal Their Customers)

### Vapi

| Dimension | Assessment |
|---|---|
| Position | Developer-focused voice AI platform. $20M+ funding. Popular in developer/startup segment. API-first. |
| Capabilities | Voice agent orchestration. Connects STT, LLM, TTS via API. Phone integration (via Twilio/Vonage). Dashboard for agent management. |
| Weakness | Pure orchestration with zero owned infrastructure. Every call traverses: Vapi -> Twilio -> Deepgram -> OpenAI -> ElevenLabs/PlayHT. Maximum Frankenstack. Latency structurally high. Reliability structurally low. No carrier licenses. No STIR/SHAKEN. Margin structure fragile - paying retail to 4+ vendors and marking up. |
| Attack angle | "Vapi is a UI on top of a Frankenstack." Target developers with: pipeline latency comparison, cost comparison showing stacked vendor margins, migration guides. Content: "What happens when your Vapi agent needs to scale to 10,000 concurrent calls." |

### Retell AI

| Dimension | Assessment |
|---|---|
| Position | "Humanlike, voice-first conversational AI." Claims ~600ms latency as "industry-leading." Healthcare wins (Pine Park Health, Medical Data Systems). |
| Capabilities | Drag-and-drop agent builder. Real-time function calling. RAG. Batch calling. SIP trunking (bring your own telephony). Branded caller ID. |
| Weakness | Does not own telephony. Relies on external carriers. ~600ms is best case; real-world is higher. No carrier licenses. Their "industry-leading" 600ms reveals how high the bar is in multi-vendor architectures. |
| Attack angle | "Retell's 'industry-leading' 600ms is our baseline." Target customers hitting scale limits. Content: latency benchmarks, "Why 600ms isn't fast enough for production voice AI." |

### Bland AI

| Dimension | Assessment |
|---|---|
| Position | Enterprise-focused. Millions of calls automated. 65%+ first-call resolution. Healthcare, financial services, insurance. |
| Capabilities | Self-hosted infrastructure. Proprietary transcription, inference, TTS on V100 GPUs. "Global Voice Delivery Network." Dedicated instances. On-premise option. |
| Weakness | Owns compute, not telecom. Self-hosted AI models, not self-hosted telephony. Still depends on external carriers for PSTN. No carrier licenses. No number inventory. V100s are previous-generation (2017 architecture). Claims "no third-party provider" for data but routes calls through third-party carriers. |
| Attack angle | "Bland self-hosts the AI. Telnyx self-hosts the AI AND the network." Target enterprise customers who care about true end-to-end control. Content: "What 'self-hosted' really means in voice AI." |

## Tier 3: Future Infrastructure Threat

### Cloudflare

| Dimension | Assessment |
|---|---|
| Position | $1.8B+ revenue. Global edge network in 310+ cities. Launched "Cloudflare Realtime" - SFU + RealtimeKit for live video/voice. Workers AI for edge inference. R2 for storage. AI Gateway for model routing. |
| Capabilities | WebRTC media routing (Realtime SFU), TURN service, RealtimeKit SDKs. Workers AI: edge inference for LLMs. No voice AI product yet - but pieces are assembling. |
| Why they're a threat | Global edge compute (310+ cities), inference at edge (Workers AI), real-time media routing, and developer mindshare. If they add telephony (PSTN origination/termination) and voice AI models, they could build a Telnyx-like integrated stack on a 10x larger network. |
| Weakness (current) | No telecom infrastructure. No carrier licenses. No PSTN connectivity. No voice AI models. Realtime is WebRTC-only - routes media between browsers, not between AI agents and phone networks. Getting into telecom requires regulatory licensing, carrier interconnects, number provisioning - a multi-year build. Workers AI runs lightweight models, not heavy STT/TTS/LLM stacks. |
| Defense strategy | Move fast. Establish "Voice AI Infrastructure" as category before Cloudflare assembles the pieces. Telnyx's moat is the telecom layer - carrier licenses, STIR/SHAKEN, number inventory, regulatory standing. Even if Cloudflare builds edge inference + WebRTC, they can't replicate the PSTN layer without becoming a carrier. Monitor: any Cloudflare announcement involving telephony, voice AI, or carrier partnerships warrants immediate competitive response. |
