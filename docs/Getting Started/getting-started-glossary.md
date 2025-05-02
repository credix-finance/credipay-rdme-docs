---
title: Glossary
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
Throughout the documentation, we have a few commonly used terms. The proper understanding of those is key for getting the main concepts clear while integrating the CrediPay API. Find below the definition of the main terms:

- **Seller**: The entity who owns the e-commerce/marketplace platform in which CrediPay will be integrated.
- **Buyer**: The seller's customer, the one who will access the platform and make a purchase.
- **Order**: The representation of the buyer's purchase inside CrediPay. The main purpose of an order is to 'reserve' credit limit for that buyer.
- **Invoice**: The representation of the Nota Fiscal XML inside CrediPay. Will always be linked to an order.
- **Installments**: One invoice might be paid in one or multiple installments. An installments is basically an amount of money which is expected to be paid at a certain date.
- **Order Cancelation**: An order can be canceled if it does not have an invoice linked to it. When the cancelation happens, the buyer's available credit limit is increased by the amount of said order.
- **Refund**: An order can be refunded if it has an invoice linked to it, and for some reason (damaged goods, misplacement, etc.) the buyer will not pay for either part or all of it.
- **(Total) Credit Limit**: The maximum amount, in BRL, a certain buyer can have outstanding to be paid to CrediPay
- **Used Credit Limit**: How much a certain buyer currently has open, to be paid to CrediPay. Sum of all open orders
- **Available Credit Limit**: How much a certain buyer can still use for financing their orders. Calculated by (Total) Credit Limit - Used Credit Limit
- **Order Payment term**: The number of days between the purchase date, and the date when the buyer needs to settle the amounts with CrediPay
- **Maximum payment term**: The maximum number of days a buyer can choose for his Order Payment Terms