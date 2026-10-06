# International Standards Review — Automation Blueprints
**Reviewed:** 2026-10-06 | **Standard:** production-readiness checklist used by agencies shipping client automations (error handling, input validation, idempotency, messaging compliance, monitoring, secrets hygiene)
**Scope:** all templates in this repo (n8n × 2, Make × 2, Zapier guides × 2, Vapi × 1)

## Verdict per platform

| Platform | Grade | Summary |
|---|---|---|
| n8n workflows | B+ → **A- after fixes** | Solid structure; was missing error workflow + input validation |
| Make blueprints | B → **A- after fixes** | Good logic; was missing error handlers + dedupe |
| Zapier guides | B | Honest about free-plan limits; 15-min polling disclosed; fine for SMB demos |
| Vapi voice config | B+ → **A after fixes** | Strong prompt design; was missing voicemail handling + real booking tool |

## Critical gaps (fixed)

### 1. No error handling — silent failures lose leads
**Standard:** every production workflow needs a failure path — the owner must know within minutes when automation breaks, otherwise leads vanish silently and the client churns.
**Was:** if Twilio/OpenAI/Sheets failed, nothing alerted anyone.
**Fix:** new `n8n/n8n-error-handler.json` — attach as the Error Workflow (Settings → Error Workflow) on every n8n workflow. Catches any node failure → instant Slack + email alert with workflow name, node, and error message. Make blueprints: error-handler notes added (right-click module → Add error handler → Break/Ignore paths). Zapier: noted as free-plan limitation.

### 2. SMS compliance — legal risk
**Standard (US TCPA):** business SMS needs prior express consent; every message must identify the sender and offer opt-out ("Reply STOP to end"). Fines: **$500-$1,500 per message**. EU/UK GDPR: same principle.
**Was:** SMS templates had no opt-out language.
**Fix:** all SMS templates now end with "Reply STOP to opt out." Setup guides now require the consent checkbox on forms (our GHL demo forms already have SMS-consent checkboxes — referenced).

### 3. No idempotency — webhook retries double-send
**Standard:** webhooks retry on timeout; without dedupe, one missed call = two apology SMS = unprofessional.
**Was:** no dedupe anywhere.
**Fix:** documented pattern in each README section — dedupe key = `phone + event type + 5-minute window` (n8n: IF + static data / Redis; Make: Data Store "Check existence"; Vapi: call ID is naturally unique).

## High gaps (fixed)

### 4. No input validation — malformed payloads burn AI credits
**Standard:** validate at the edge before calling paid APIs.
**Was:** AI qualifier sent whatever the webhook received straight to OpenAI.
**Fix:** `n8n-ai-lead-qualifier.json` now has a **"Has Contact Info?"** gate — drops payloads with no email AND no phone, logs them as `invalid` instead of spending OpenAI credits.

### 5. Vapi couldn't actually book — demo promised booking
**Standard:** a receptionist that can't book is a FAQ bot; the #1 buyer question is "does it put it in my calendar?"
**Was:** config collected booking details but had no tool to act on them.
**Fix:** `vapi-dental-receptionist.json` now includes a **`bookAppointment` function tool** (POSTs name/phone/day/type to your webhook → n8n/Make/GHL creates the appointment), plus `voicemailDetection` with a voicemail message, `endCallMessage`, and background denoising.

### 6. WhatsApp gap — the most in-demand combo had zero coverage
**Demand signal:** bovo-digital 2026 — the **n8n + Vapi + WhatsApp + CRM** combination is the single most in-demand automation skill (€750-900/day band). Our repo had nothing on WhatsApp.
**Fix:** new `n8n/n8n-whatsapp-ai-auto-reply.json` — WhatsApp Business Cloud webhook → AI replies in the customer's language → hot intents (booking/price) escalate to the owner. Uses the Meta WhatsApp Cloud API free tier (1,000 conversations/month free).

## Medium gaps (documented, not blocking)

7. **Zapier "instant" vs 15-min free polling** — already disclosed in the guides; honest framing kept.
8. **No monitoring dashboard** — n8n execution history + Vapi call logs cover it at this scale; noted as a future add (Grafana/Uptime Kuma) for agency scale.
9. **GHL integration via raw HTTP, not native node** — deliberate: no credential assumptions in templates; the GHL API shape is documented in the sticky notes.
10. **No HubSpot/Salesforce variant** — demand exists (€650-800/day CRM AI band); listed as next build if a prospect asks.

## Demand mapping — what sells fastest, in order
1. **Vapi voice receptionist** (fixed: real booking tool) → demo it live on a call; highest rate band
2. **WhatsApp AI auto-reply** (new) → every home-service/dental prospect understands WhatsApp instantly
3. **Missed-call → SMS → CRM** (fixed: compliant + monitored) → the 60-second pitch that never fails
4. **AI lead scoring** (fixed: validated) → agencies and multi-location businesses
5. **Review requests** → cheapest to sell, fastest to deploy, feeds Google rankings

## Compliance checklist for every client deployment
- [ ] SMS consent checkbox on the form (opt-in proof stored)
- [ ] "Reply STOP to opt out" in every automated SMS
- [ ] Business name in every message (sender identification)
- [ ] Error workflow attached and tested (send a bad payload, confirm the alert fires)
- [ ] Dedupe key configured on every webhook
- [ ] Vapi call recording disclosure per local law (some US states require two-party consent — the greeting should state "this call may be recorded")
