---
title: Order and Installment statuses
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
In CrediPay, we work with two main status flows: one for Orders, and another one for Installments. Find below a description of each of flows:

## Orders

1. **Created**: Once the POST v1/orders endpoint is called successfully, a new order will be created in CrediPay, with the _Created_ status.
2. **Finalized**: The integrator should call the POST v1/orders/{orderId}/finalize endpoint once the order is confirmed and ready to be shipped. This will cause the order to move to the _Finalized_ status. In some scenarios this might not be needed, make sure to align with your CrediPay representantive.
3. **Captured**: This is the last status of the order flow and it happens once an Invoice is attached to the order via the POST v1/invoices. After that, the Repayment entities are created and their status flow start. From this point onwards, an order cannot be cancelled.
4. **Cancelled**: An order may be cancelled through the POST v1/orders/{orderId}/cancel endpoint. A cancelled order will not take up any credit limit, and may not be "uncancelled".

<br />

## Repayments

In the Repayments status flow, no endpoint calls from the integrator are required. A repayment may have 2 main statuses:

1. **open**: CrediPay has a pending charge for that repayment, which hasn't been paid yet.
2. **paid**: CrediPay has been paid, in a timestamp stored in the payment_date field. This means that the full Order and Status lifecycle has reached its end.

<br />

## Refunds

What you will also find in our APIs is the refund_status, which reflects if the original charge amount was changed or not - usually because of delivery issues, damaged goods, etc. There are 3 main refund statuses:

1. **NoRefund**: The original amounts stands, no refund has been issued.
2. **PartialRefund**: There was a partial deduction in the original amount
3. **FullRefund**: There was a full cancellation of the charge.