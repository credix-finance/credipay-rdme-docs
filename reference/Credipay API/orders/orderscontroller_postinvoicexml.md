---
title: Create an order by NF-e
excerpt: >-
  Allows you to create an order by submitting a Nota Fiscal XML file. If orderId
  is not provided, a new order is created. If orderId is provided, the invoice
  is linked to the specified order. For an invoice to be accepted, it needs to
  be within the buyer's available credit limit and maximum payment terms.
api:
  file: open-api.yaml
  operationId: OrdersController_postInvoiceXml
hidden: false
---