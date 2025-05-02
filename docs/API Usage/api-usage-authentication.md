---
title: Authentication
excerpt: Learn how to authenticate with the CrediPay API.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
CrediPay's API uses API keys to authenticate requests. You can request an API key by contacting us at [suporte-credipay@credix.finance](suporte-credipay@credix.finance)

> 🚧 Don't share your API key in publicly accessible areas
> 
> API keys carry many privileges, so be sure to keep them secure!

## Authenticating an API request

To authenticate an API request, you should provide your API key in the `X-CREDIPAY-API-KEY` header.

For example:

```curl
curl --request GET \
--url https://api.credix.finance/v1/buyers/70631413000079 \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'X-CREDIPAY-API-KEY: YOUR_API_KEY'
```

The response will be a JSON.

```json
{
  "taxId": "70631413000079",
  "name": "ACME ltda.",
  "sellerConfigs": [
    {
      "taxId": "82356350000079",
      "maxPaymentTermDays": 30,
      "monthlyDiscountRate": 0.03,
      "transactionFeePercentage": 0.02
    }
  ],
  "creditLimitAmountCents": 1020000,
  "availableCreditLimitAmountCents": 820000,
  "onboarded": false,
  "eligible": false
```