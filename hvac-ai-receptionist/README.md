# HVAC AI Receptionist + Missed Call Text-Back (n8n)

Professional starter templates for an HVAC service business.

## Included workflows
- `n8n_hvac_ai_receptionist.json`: receives a voice-agent webhook, normalizes common fields, validates the caller phone, and optionally forwards a lead to a configured CRM endpoint.
- `n8n_hvac_missed_call_textback.json`: receives a missed-call event, checks phone, consent, opt-out and call status, then calls a configurable SMS provider endpoint.

## Important
These are integration templates, not ready-to-run production systems. Workflows are inactive by default. You must configure your voice-agent webhook, CRM destination, SMS provider URL, authentication and sender number. They have not been tested against your particular provider payload.

## Import and configure
1. In n8n, choose **Import from File** and import each JSON.
2. Open each Webhook node and use its **Test URL** first.
3. Send a sample payload and inspect the actual incoming JSON; map fields to your chosen provider.
4. For lead forwarding, configure `HVAC_LEAD_DESTINATION_URL` or replace the example destination. Keep the CRM-forwarding node disabled until configured.
5. For SMS, replace the placeholder API endpoint, authentication, sender number and payload with your provider's documented format. Prefer n8n credentials over hard-coded API keys.
6. Test with your own phone and consented test contacts. Keep workflows inactive until verified.

## Example missed-call payload
```json
{
  "call_id": "demo-missed-001",
  "phone": "+15551234567",
  "customer_name": "Jordan",
  "business_name": "Example HVAC",
  "call_status": "missed",
  "consent_to_text": true,
  "opted_out": false
}
```

## Production checklist
- Use HTTPS and provider-supported webhook authentication/signature verification.
- Add duplicate-event protection and durable CRM storage.
- Implement opt-out handling and honor STOP. Verify customer consent and applicable TCPA, carrier and privacy requirements before texting.
- Never claim a booking is confirmed unless the scheduling system confirms it.
- Avoid HVAC diagnosis, safety assurances, or fixed repair quotes from AI; collect symptoms and route to a qualified technician.
- Never commit API keys, credentials, or real customer data to GitHub.
