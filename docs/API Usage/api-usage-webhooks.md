---
title: Webhooks
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Webhooks Documentation

Webhooks enable services to notify one another of events in real-time. They operate as a POST request sent to a pre-configured endpoint. This guide will help you understand the available webhook events, how to configure and test endpoints, verify signatures, manage retries, and troubleshoot issues.

***

## Introduction

Webhooks are an efficient way for systems to notify one another of specific events. When an event occurs, a webhook sends a POST request to a designated endpoint with relevant details.

* **Endpoint Setup**: Define a URL for receiving webhook events. Typically, one endpoint handles all event types.
* **Processing Webhooks**: Respond with a 2xx HTTP status code to confirm successful processing within 15 seconds.
* **Security Considerations**: Verify the signature and timestamp of the webhook payload to ensure authenticity.
* **Disabling CSRF Protection**: Disable CSRF protection for the endpoint if your framework enables it by default.

***

## Events and Event Types

### Overview

Webhooks notify you of specific events related to orders and repayments. Below are the available event types:

| Name                | Description                                                                                   |
| ------------------- | --------------------------------------------------------------------------------------------- |
| `order.accepted`    | Triggered when an order is confirmed.                                                         |
| `order.rejected`    | Triggered when an order is rejected.                                                          |
| `repayment.created` | Triggered when a new repayment is created (e.g., invoice upload, refunds, or renegotiation).  |
| `repayment.settled` | Triggered when a repayment is settled (e.g., buyer payment or full refund of an installment). |

### Payload Schemas

Each event type includes a JSON payload with event-specific details. Refer to the [Event Catalog](https://app.credipay.credix.finance/webhooks/) for schema definitions and examples.

***

## Adding an Endpoint

### Steps to Add an Endpoint

1. Provide a URL that your system controls.
2. Select the event types you want to receive notifications for.
3. If no event types are specified, the endpoint will receive all events by default.

***

## Testing Endpoints

Once an endpoint is added, test it to ensure it’s functioning as expected:

1. Navigate to the "Testing" tab.
2. Send a test event to your endpoint.
3. Inspect the payload and response status of the event.
4. Validate that the endpoint handles the payload correctly.

***

## Signature Verification

Webhook signatures verify the authenticity of webhook messages. Each message includes a signature generated using your secret key.

### Steps to Verify Signatures

1. Extract the `svix-id`, `svix-timestamp`, and `svix-signature` from the webhook headers.
2. Use a library, such as Svix, to verify the payload using your secret key.

#### JavaScript Example

```javascript
import { Webhook } from "svix";

const secret = "whsec_YOUR_SECRET_KEY";
const headers = {
    "svix-id": "msg_ID",
    "svix-timestamp": "1614265330",
    "svix-signature": "v1,SIGNATURE_HERE",
};
const payload = '{"example": "data"}';

const wh = new Webhook(secret);
try {
    const verifiedPayload = wh.verify(payload, headers);
    console.log("Verified payload:", verifiedPayload);
} catch (err) {
    console.error("Failed to verify signature:", err);
}
```

Refer to the [Webhook Verification Documentation](https://docs.svix.com/receiving/verifying-payloads/how) for more examples.

***

## Retry Mechanism

Webhook delivery follows an exponential backoff retry schedule to ensure reliability.

### Retry Schedule

| Attempt | Time Interval     |
| ------- | ----------------- |
| 1       | Immediately       |
| 2       | 5 seconds         |
| 3       | 5 minutes         |
| 4       | 30 minutes        |
| 5       | 2 hours           |
| 6       | 5 hours           |
| 7       | 10 hours          |
| 8       | 10 hours (repeat) |

### Manual Retries

You can manually retry failed messages via the application portal. Select a message and use the "Retry" option.

***

## Failure Recovery and Event Replay

### Re-enabling Endpoints

Endpoints disabled after 5 days of failed attempts can be re-enabled via the webhook dashboard.

### Resending Messages

* Use the UI to resend individual or bulk messages for recovery.
* Recover failed webhooks using the provided APIs.

#### Recover Failed Webhooks API

**Endpoint:**

```
POST /webhook-events/endpoints/:endpointId/recover
```

**Description:**\
Attempts to recover all failed webhook events for the specified endpoint.\
[See API reference](https://docs.credipay.credix.finance/reference/post-recover-failed-webhooks)

### Example Usage

Use these APIs to programmatically recover or replay events:

```javascript
// Recover failed events
fetch(`/webhook-events/endpoints/${endpointId}/recover`, {
    method: 'POST',
    headers: { 'Authorization': `Bearer ${apiKey}` },
});
```

***

## Troubleshooting & Failure Recovery

### Common Issues

1. **Using Incorrect Payloads**: Always verify the raw payload body as sent.
2. **Wrong Secret Key**: Ensure the secret key matches the configured endpoint.
3. **Improper Response Codes**: Return a 2xx status code for successful deliveries.
4. **Timeouts**: Avoid long processing times; queue the message for asynchronous handling if necessary.

### Failure Recovery

* **Re-enabling Endpoints**: Endpoints disabled after 5 days of failed attempts can be re-enabled via the webhook dashboard.
* **Resending Messages**: Use the UI to resend individual or bulk messages for recovery.

***

By following this guide, you can reliably configure, test, and manage webhooks for seamless event-driven communication.
