---
title: Refund an order
excerpt: >-
  Refunds an order. When this endpoint is called, the amount CrediPay charges
  the buyer will be reduced by the amount passed in the body. If the given order
  was advanced to the seller, the refund amount will then be subtracted from the
  next disbursement the seller receives.
api:
  file: open-api.yaml
  operationId: post-order-refund
hidden: false
---