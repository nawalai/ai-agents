# AI Appointment Booking Agent — Bloom Hair & Beauty Salon (Portfolio Demo)

## Problem
Small service businesses (salons, clinics, consultancies) typically handle appointment booking manually — a staff member has to answer messages, check calendar availability, and confirm details back and forth. This doesn't scale and depends entirely on someone being available to respond.

## What I built
A conversational AI booking agent (built for a fictional salon, "Bloom Hair & Beauty Salon," as a portfolio demonstration) that:
1. **Holds a natural, multi-turn conversation** — remembers earlier parts of the conversation (name, requested service) rather than asking the same questions repeatedly
2. **Checks real calendar availability** before confirming a booking
3. **Creates the actual calendar event** once the customer confirms all details
4. **Handles incomplete requests gracefully** — if a customer doesn't specify a date/time, it asks a clarifying follow-up instead of guessing

## Architecture
```
Chat Trigger (conversational interface)
   → AI Agent
        ├── Chat Model: Google Gemini
        ├── Memory: conversation history (Simple Memory)
        └── Tools:
              - Google Calendar: Get Many Events (check availability)
              - Google Calendar: Create Event (book the appointment)
```

This is architecturally different from my other lead-agent projects (which are single-shot: one input → one classification/output). This project uses n8n's **AI Agent** node, which lets the model autonomously decide *which* tool to call and *when*, based on the flow of conversation — closer to the full "LLM + tools + memory + goal" definition of an agent.

## Tools used
- **n8n** — AI Agent orchestration, Chat Trigger, tool integration
- **Google Gemini** — conversational reasoning and tool-call decisions
- **Google Calendar API** — real-time availability checking and event creation

## Key implementation detail
Fields like appointment start/end time aren't hardcoded — they're marked as **AI-controlled** (via n8n's per-field toggle), meaning the model fills them in dynamically based on what the customer actually says in conversation, rather than a fixed expression.

## Outcome
A working conversational agent that took a request like *"I want a haircut this Thursday at 2pm"*, checked real calendar availability, asked for the customer's name and email, and created an actual calendar event — demonstrated live in the linked demo.

📹 [Demo video](./demo.mp4)
🖼️ [Screenshots](./screenshots/)
📄 [Exported workflow (JSON)](./bloom-booking-agent.json)
