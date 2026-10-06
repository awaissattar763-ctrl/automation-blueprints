# Zap 1: New Lead → Instant SMS Alert + Spreadsheet Log
**Time to build:** ~10 minutes | **Zapier free plan:** OK (2 steps used)

> Zapier has no JSON import, so follow these exact steps. Works on the free plan (100 tasks/month).

## What it does
The second someone submits your website/GoHighLevel form, the business owner gets an instant SMS and the lead is logged — no lead waits until morning.

## Steps

### Step 1 — Trigger: Webhooks by Zapier
1. Create a new Zap → Trigger: **Webhooks by Zapier** → Event: **Catch Hook**
2. Copy the webhook URL Zapier gives you.
3. Paste it as the webhook target in your form (GoHighLevel workflow webhook, WordPress form, etc.).
4. Send a test submission → Zapier should show sample data: `name`, `phone`, `email`, `service`.

### Step 2 — Action: SMS by Zapier (or Twilio)
**Option A (no Twilio account):** Action: **SMS by Zapier** → Send SMS
- To: your business mobile number
- Message: `New lead: {{name}} ({{phone}}) — {{service}}. Reply fast!`

**Option B (Twilio):** Action: **Twilio** → Send SMS
- From: your Twilio number
- To: your business mobile
- Message: same as above

### Step 3 — (free-plan workaround for logging)
The free plan allows only 2 steps, so logging goes in a **second Zap**:
- Zap 1b Trigger: same Catch Hook URL pattern (use **Paths** on paid, or duplicate the webhook)
- Simpler: upgrade-free alternative — use the **n8n version** of this flow in this repo (`n8n/n8n-missed-call-sms-crm.json`) which does SMS + CRM + Slack in one workflow for free.

## Test it
Submit your own form → you should get the SMS within ~2 minutes (free plan polls every 15 min; paid is instant).

## Client pitch line
"Every lead you get is answered in under 60 seconds — while you sleep."
