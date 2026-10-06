# Zap 2: Finished Job → Automatic Review Request Sequence
**Time to build:** ~15 minutes | **Zapier free plan:** needs 2 Zaps (or 1 multi-step on paid)

> Businesses with 50+ Google reviews get dramatically more calls. This Zap asks for the review automatically — owners always forget to ask manually.

## What it does
When a job is marked "won/complete" (in your CRM, spreadsheet, or GoHighLevel pipeline), the customer automatically gets a polite review request by SMS/email 2 hours later.

## Steps

### Zap A — Catch the completed job
1. Trigger: **Webhooks by Zapier** → **Catch Hook**
   - Fire this webhook from GoHighLevel when an opportunity hits "Job Won" (Workflow → Webhook action), or add a row to Google Sheets manually.
   - Expected data: `name`, `phone`, `email`, `service`
2. Action: **Delay by Zapier** → Delay For: **2 hours**
   - (Gives the customer time to get home and feel good about the job.)

### Zap B — Send the review request (separate Zap, same trigger data)
Because the free plan is 2-step, chain it: Zap A's final step can be another webhook POST to Zap B's Catch Hook.
1. Trigger: **Webhooks by Zapier** → **Catch Hook**
2. Action: **SMS by Zapier** (or Twilio / Gmail):
   - Message: `Hi {{name}}, thanks for choosing {{BUSINESS}}! If you were happy with the {{service}} today, a quick Google review would mean the world to us: {{REVIEW_LINK }}`
   - Email version subject: `How did we do today?`

### The review link
Get it from the business's Google Business Profile → Share → short link. Put it in the message.

## Test it
Move a test opportunity to "Won" → 2 hours later you get the SMS.

## Client pitch line
"Happy customers forget to leave reviews. This asks every single one — automatically."
