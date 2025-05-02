---
title: Create an order
excerpt: >-
  Tries to create a new order. Will work if the buyer has enough credit limit
  and payment terms for the given order. Once successfully created, the total
  amount of the order will be subtracted from the buyer's available credit
  limit.
api:
  file: credipay-api.json
  operationId: post-create-order
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: endpoint
      slug: post-cancel-order
      title: Cancel an order
---
Use this endpoint after a customer places an order on your website so that CrediPay can provision the amount to be financed.

For an order to be successfully created, two conditions need to be met:

- The order's payment terms cannot exceed CrediPay's approved payment terms for this customer.  
- The order's total (subtotalAmountCents + taxAmountCents + shippingCostCents) amount cannot exceed CrediPay's approved credit limit for this customer.

The values for the above conditions can be fetched from`/buyers/{buyer_CNPJ}?sellerTaxId={seller_CNPJ}`

Remember: once an order is created, that customer's available credit limit will be subtracted from the order's Total. If, for some reason, it was created incorrectly, you should cancel it using the `/orders/{order_id}/cancel`endpoint to free up the limit.