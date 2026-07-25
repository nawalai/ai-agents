# AI Voice Calling Agent — ProperCareOnline

## Problem
ProperCareOnline (a virtual assistant/outsourcing agency serving property managers, landlords, and short-term rental hosts) had no way to capture and prioritize leads that come in over the phone — every inbound call required a human to answer, ask qualifying questions, and manually follow up, with no consistent process for flagging urgent, high-value callers.

## What I built
A fully automated AI voice agent that:
1. **Answers real phone conversations** using a natural-sounding AI voice assistant (Vapi), following a scripted persona for ProperCareOnline
2. **Filters out noise** — Vapi sends multiple webhook events per call (status updates, speech updates); the workflow filters for only the final "end-of-call-report" event before doing any expensive processing
3. **Extracts structured data from unstructured speech** — pulls caller name, company, email, and service interest directly out of a raw conversation transcript using an LLM
4. **Classifies lead urgency** (HOT / WARM / COLD) based on signals like urgency, number of units/properties mentioned, and stated timelines
5. **Validates extracted data** before acting on it — checks that an email address is actually well-formed before attempting to send a reply, preventing failures when a caller doesn't share contact details
6. **Routes automatically**: HOT leads trigger an internal notification email with full call context; other leads receive an automated, personalized follow-up email referencing their specific inquiry and the one-week free trial

## Architecture
```
Vapi (voice AI + telephony)
   → Webhook (n8n)
   → Filter for end-of-call-report only
   → LLM extraction + classification (Google Gemini)
   → Parse into structured fields
   → Switch (HOT vs. other)
   → Validate email format
   → Route to internal alert or automated customer reply (Gmail)
```

## Tools used
- **Vapi** — real-time voice AI, speech-to-text, text-to-speech, and telephony (free tier: no-cost US number + trial credits)
- **n8n** — workflow orchestration, webhook handling, conditional routing
- **Google Gemini** — natural language extraction and lead classification
- **Gmail API** — automated notifications and customer replies
- **ngrok** — local tunnel for webhook development/testing

## Engineering challenges solved
- **Event noise filtering**: Vapi fires several webhook events per call; without filtering, this triggered redundant AI calls and hit rate limits. Solved with an IF node checking specifically for the `end-of-call-report` event type.
- **Model availability changes**: Google periodically deprecates/restricts specific Gemini model versions for new accounts; built resilience by testing multiple model options and adding automatic retry logic.
- **Malformed data handling**: since voice conversations don't guarantee complete information (callers sometimes hang up before sharing an email), added explicit validation before attempting downstream actions, rather than letting the workflow fail silently.
- **International telephony limits**: Vapi's free-tier number doesn't support outbound international calls; validated the full pipeline using Vapi's live conversational testing interface, which exercises the identical AI/webhook/processing pipeline as a real phone call.

## Outcome
A working, end-to-end voice AI agent that can hold a natural phone conversation, understand caller intent, and automatically route the lead appropriately — demonstrated live with real test calls, screenshots, and a recorded demo (linked below).

📹 [Demo video](./demo.mp4)
🖼️ [Screenshots](./screenshots/)
📄 [Exported n8n workflow (JSON)](./propercareonline-voice-agent.json)
