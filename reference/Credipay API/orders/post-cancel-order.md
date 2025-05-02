---
title: Cancel an order
excerpt: >-
  Moves an order to cancelled state and increases the buyer's available credit
  limit by that order's total amount. If the order already has an invoice linked
  to it, it will be fully refunded.
api:
  file: credipay-api.json
  operationId: post-cancel-order
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Once an order is cancelled, its respective buyer gets the total amount of the order back in their available credit limit. An order cannot be cancelled if it already contains an invoice linked to it.