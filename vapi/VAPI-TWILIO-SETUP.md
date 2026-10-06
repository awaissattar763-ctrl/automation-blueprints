# Vapi + Twilio Setup Guide — Live AI Voice Receptionist
**Cost to try:** $0 — Vapi gives **$10 free credit** on signup (no card needed, ~150-200 minutes of talk time). Twilio trial gives **$15 credit**.

## What you get
A real phone number that answers with an AI receptionist, books appointments, handles emergencies, and logs every call — the exact demo to show dental / home-service / law prospects.

## Step 1 — Create your Vapi account (5 min)
1. Go to **dashboard.vapi.ai** → Sign Up (Google or email).
2. Your **$10 free credit is already loaded** — no credit card required.
3. Go to **Assistants → Create Assistant → Import** (or paste config manually).

## Step 2 — Load the receptionist config
1. Open `vapi/vapi-dental-receptionist.json` in this repo.
2. In Vapi: **Assistants → + New → Import JSON** → paste the file contents → Save.
3. What is inside:
   - **Model:** gpt-4o-mini (cheap, fast, good enough for reception work)
   - **Voice:** ElevenLabs "sarah" (natural female voice)
   - **Transcriber:** Deepgram nova-2
   - **Behavior:** greeting → emergency triage → booking (name/phone/day/type) → confirmation
   - **Post-call extraction:** structured data (name, phone, appointment type, isEmergency) auto-saved per call
4. Click **Talk to assistant** in the dashboard to test it in your browser — free, uses your credit.

## Step 3 — Get a real phone number via Twilio (10 min)
1. Sign up at **twilio.com/try-twilio** → verify your email + phone number.
2. You get **$15 trial credit**. Buy a phone number: **Phone Numbers → Buy a Number** (~$1.15/month US local).
   - Trial numbers can only call verified numbers — fine for demos.
3. In Vapi: **Phone Numbers → Import → Twilio** → paste your Twilio Account SID + Auth Token → select your number → attach it to the assistant.

## Step 4 — Test a real call
Call your Twilio number from your own phone. Nora answers, books a fake appointment, and you will see the transcript + extracted data in **Vapi → Calls**.

## What it costs after free credits
| Item | Cost |
|---|---|
| Vapi hosting | $0.05/min |
| Everything else (STT + LLM + TTS) | ~$0.03-0.08/min passed through |
| **Total per minute** | **~$0.08-0.13** |
| 3-minute booking call | ~$0.25-0.40 |
| 500 calls/month (3 min avg) | ~$75-175/month |

A human receptionist costs $3,000+/month. That math is your sales pitch.

## Client demo script (60 seconds)
1. "Can I call your demo number right now?" → let them call it.
2. They hear Nora book an appointment → show them the transcript + extracted lead data in Vapi dashboard.
3. "This replaces missed calls, after-hours voicemail, and the front-desk salary — for about $100/month in usage."

## Going further
- Connect Vapi **tools** to GoHighLevel: real appointment booking via webhook (see `n8n/` workflows for the pattern).
- Swap voices in one click (11labs voices). Add Spanish with a second assistant.
- For outbound (appointment reminders), use Vapi's batch-call API.
