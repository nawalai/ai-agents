# AI Agents Portfolio — Nawal Shahid

Hi, I'm Nawal — I build practical, working AI agents using no-code/low-code tools (n8n, Google Gemini, Vapi) to solve real business problems. Below are automations I've built end-to-end, including for my own business.

📧 nawalsalman1603@gmail.com | 📍 Lahore, Pakistan

---

## Project 1: FAQ Chatbot — Sparkling Spot (Jewelry & Handmade Bags)

**Problem:** Sparkling Spot (my jewelry and handmade crochet bags store) needed a way to instantly answer common customer questions about products, payment, and delivery without manual replies for every inquiry.

**What I built:** An FAQ knowledge base covering jewelry, custom handmade bags, and store policies — including different payment logic (COD for jewelry, advance payment for custom handmade bags) — ready to plug into a chatbot interface.

**Tools used:** Content structuring for chatbot knowledge bases (Voiceflow/Claude Project compatible)

📄 [View FAQ content](./sparkling-spot-faq/SparklingSpot_FAQ.md)

---

## Project 2: Lead Qualification & Auto-Response Agent — ProperCareOnline

**Problem:** ProperCareOnline (a virtual assistant/outsourcing agency) receives inbound leads through a contact form but has no automatic way to prioritize urgent, high-value inquiries over casual browsers.

**What I built:** A fully automated n8n workflow that:
1. Detects new leads from a Google Form/Sheet in real time
2. Uses Google Gemini to classify each lead as **HOT / WARM / COLD** based on urgency, scale, and specificity of their inquiry
3. Automatically drafts a personalized reply matched to their specific service interest
4. Routes HOT leads to an internal urgent-notification email, while WARM/COLD leads receive an automatic personalized reply
5. Includes automatic retry and fallback-model logic so temporary AI service outages don't break the workflow

**Tools used:** n8n, Google Gemini API, Google Sheets, Gmail

📄 [View exported workflow (JSON)](./propercare-lead-agent/propercare-lead-agent.json)
🖼️ [View workflow screenshots](./propercare-lead-agent/screenshots/)

---

## Project 3: AI Voice Calling Agent — ProperCareOnline

**Problem:** ProperCareOnline had no way to capture and prioritize leads coming in over the phone — every call required a human to answer, qualify, and manually follow up.

**What I built:** A live AI voice agent that:
1. Answers real phone conversations using a natural-sounding AI assistant (Vapi)
2. Filters Vapi's multiple webhook events per call down to just the final call outcome
3. Extracts caller name, company, email, and service interest directly from the raw conversation transcript using an LLM
4. Classifies lead urgency (HOT / WARM / COLD) the same way as my text-based lead agent, but from spoken conversation instead of form data
5. Validates extracted data before acting (e.g., checks for a real email format before attempting to send a reply)
6. Routes HOT leads to an internal alert, and sends other leads an automated personalized follow-up

**Why this matters:** This is the most technically demanding project in this portfolio — it handles real-time voice conversation (not just text), filters noisy multi-event webhooks, and gracefully handles incomplete data from live, unscripted speech.

**Tools used:** Vapi (voice AI, telephony), n8n, Google Gemini, Gmail

📹 [Demo video](./propercareonline-voice-agent/demo.mp4)
🖼️ [Screenshots](./propercareonline-voice-agent/screenshots/)
📄 [Exported workflow (JSON)](./propercareonline-voice-agent/propercareonline-voice-agent.json)
📝 [Full case study](./propercareonline-voice-agent/README.md)

---

## Project 4: AI Appointment Booking Agent — Bloom Hair & Beauty Salon (Portfolio Demo)

**Problem:** Small service businesses handle appointment booking manually — checking calendar availability and confirming details back and forth requires a staff member to be available for every request.

**What I built:** A conversational AI agent (built for a fictional salon as a portfolio demonstration) that:
1. Holds a natural, multi-turn conversation, remembering earlier context instead of re-asking questions
2. Checks real Google Calendar availability before confirming a booking
3. Creates the actual calendar event once the customer confirms all details
4. Asks clarifying follow-up questions when a request is incomplete, rather than guessing

**Why this matters:** Unlike my other lead-agent projects (single-shot classification), this uses n8n's **AI Agent** architecture — Chat Model + Memory + Tools — where the model autonomously decides which tool to call and when, based on the live conversation. This is the fullest expression of "LLM + tools + memory + goal" in this portfolio.

**Tools used:** n8n (AI Agent, Chat Trigger), Google Gemini, Google Calendar API

📹 [Demo video](./bloom-booking-agent/demo.mp4)
🖼️ [Screenshots](./bloom-booking-agent/screenshots/)
📄 [Exported workflow (JSON)](./bloom-booking-agent/bloom-booking-agent.json)
📝 [Full case study](./bloom-booking-agent/README.md)

---

## Skills demonstrated across these projects
- Prompt engineering for structured, parseable AI outputs
- Conditional workflow logic (branching, routing based on AI decisions)
- API integration without code (Google Sheets, Gmail, Gemini, Vapi)
- Real-time voice AI and telephony integration
- Error handling and resilience (retries, fallback models, data validation)
- Business-first thinking: every automation solves a real, specific operational problem

## What's next
Currently building: a Google Maps lead-scraping agent that finds local businesses, extracts contact emails, and logs qualified leads automatically.
