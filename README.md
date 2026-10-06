# Automation Blueprints — n8n · Make · Zapier · Vapi

Import-ready automation templates for service businesses (dental, home services, med spa, legal). Built by [Muhammad Awais Sattar](https://awaissattar-portfolio.vercel.app/).

Every template is labeled honestly: connect your own API credentials after import. Nothing here sends real messages until you activate it with your own accounts.

## n8n (`/n8n`) — import via Workflows → Import from File
| File | What it does |
|---|---|
| `n8n-missed-call-sms-crm.json` | Missed call → instant apology SMS → contact saved to GoHighLevel → Slack alert to owner |
| `n8n-ai-lead-qualifier.json` | New lead → input validation → GPT-4o-mini scores it 0-100 → hot leads get an instant personal email, everyone is logged to Google Sheets |
| `n8n-whatsapp-ai-auto-reply.json` | WhatsApp message → AI replies in the customer's language → booking/price/urgent intents escalate to the owner instantly (Meta Cloud API free tier) |
| `n8n-error-handler.json` | **Attach to every workflow** (Settings → Error Workflow): any node failure → instant Slack + email alert. No silent failures. |

**n8n cost:** self-hosted Community = **free forever**, unlimited executions (needs a server ~$5-15/mo, or Docker locally). Cloud Starter = €20/mo (2,500 executions). 14-day Cloud trial is free.

## Make (`/make`) — import via Scenarios → Import Blueprint
| File | What it does |
|---|---|
| `make-fb-leads-instant-followup.json` | Facebook Lead Ad → instant SMS + Google Sheets log + owner email alert (3 parallel paths) |
| `make-lead-ai-qualification.json` | Webhook lead → OpenAI scores it → hot leads emailed instantly, all logged |

**Make cost:** free plan = **1,000 ops/month, $0**. Core = $9/mo (10,000 credits).

## Zapier (`/zapier`) — step-by-step build guides (Zapier has no JSON import)
| Guide | What it does |
|---|---|
| `zap-new-lead-sms-alert.md` | New form submission → instant SMS to owner (2-step, fits free plan) |
| `zap-review-request-sequence.md` | Job marked won → automatic Google-review request 2 hours later |

**Zapier cost:** free plan = **100 tasks/month**, 2-step Zaps. Professional = $19.99/mo (750 tasks).

## Voice AI (`/vapi`) — Vapi + Twilio
| File | What it does |
|---|---|
| `vapi-dental-receptionist.json` | Full voice-receptionist assistant config: greeting → emergency triage → appointment booking **via bookAppointment tool** → post-call data extraction; voicemail handling, end-call message, noise reduction |
| `VAPI-TWILIO-SETUP.md` | Complete setup: free accounts, real phone number, test call, costs, and the 60-second client demo script |

## Standards review
**[REVIEW.md](REVIEW.md)** — every template audited against production standards (error handling, input validation, idempotency, SMS compliance, monitoring). All critical and high gaps fixed.

**Voice cost to try:** **$0** — Vapi $10 free credit (no card) + Twilio $15 trial credit. Live cost after: ~$0.08-0.13/min (~$0.25-0.40 per 3-min call).

## Why these four platforms?
Clients do not buy "automation" — they buy *missed calls answered, leads followed up, reviews collected*. Each blueprint maps to one of those outcomes, and together they cover whatever stack a prospect already uses.

## License
Templates are free to use and adapt. Your API keys and credentials stay yours.
