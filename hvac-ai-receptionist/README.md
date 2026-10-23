# HVAC AI Receptionist + Missed-Call Text-Back (n8n)

Professional starter kit for an HVAC service business. Includes importable n8n workflows for:
1. Capturing AI receptionist call summaries/leads via webhook.
2. Sending a missed-call text-back through a configurable SMS provider HTTP endpoint.
3. Normalizing/validating inputs and returning explicit webhook responses.

## Important
These are integration templates. They are not live until you configure your voice-agent webhook, SMS provider endpoint/API key, business phone number, and your data destination. Test using provider test payloads before activating. No API keys should be committed to GitHub.

## Workflow files
- `n8n_hvac_ai_receptionist.json`
- `n8n_hvac_missed_call_textback.json`

## Configure
1. In n8n, use **Import from File** for each JSON.
2. Open the webhook node and copy the Test URL first.
3. Send a sample payload to the Test URL, inspect the incoming JSON, and map provider fields if needed.
4. For the receptionist workflow, connect your voice agent to the lead-capture webhook and configure the owner-alert endpoint/node of your choice.
5. For missed-call texts, configure the SMS HTTP Request node with your provider's documented endpoint, authentication, and sender number. The template uses placeholder credentials and a placeholder URL.
6. Test with your own phone and consented test contacts before production.

## Suggested incoming fields
```json
{
  "call_id": "demo-call-001",
  "customer_name": "Jordan Smith",
  "phone": "+15551234567",
  "service_address": "123 Example St",
  "city": "Austin",
  "zip_code": "78701",
  "issue_type": "AC not cooling",
  "urgency": "same_day",
  "preferred_time": "afternoon",
  "booking_status": "requested",
  "summary": "Customer says AC is running but not cooling.",
  "consent_to_text": true
}
```

## Safety and compliance notes
- Never claim an appointment is confirmed unless an actual scheduling system confirms it.
- Do not ask the AI to diagnose HVAC equipment or quote final repair prices. Have it collect symptoms and route to a technician.
- Text only contacts where you have the necessary permission. Honor opt-outs such as STOP and follow applicable TCPA/carrier rules.
- Do not put real customer data, API tokens, phone numbers, or credentials in GitHub.
