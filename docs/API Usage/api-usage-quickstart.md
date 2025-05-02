---
title: Quickstart guide
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
## Introduction

With CrediPay, any marketplace or e-commerce can provide credit services to its customers in 3 simple integration steps. This page will outline each of those steps for an integration quickstart. For more details, please check each endpoint's section in the sidebar.

## Step 0: Set up API Key

If you haven't already, please check the [Authentication](doc:api-usage-authentication) page to see how you can set up an API Key. This will be needed for all the endpoint calls listed below.

<br />

## Step 1: Check Buyer

Whenever a customer goes to your checkout page, you should call our GET Buyer endpoint. This endpoint will assess if they are approved by CrediPay, and if so, which would be the details of their order. The order should be within that buyer's available credit limit and payment terms.

[More details](/reference/get-buyers)

> 📘 Pre-approval of buyers
>
> CrediPay works by pre approving credit limits and payment terms for buyers. In case you haven't already, please reach out to your CrediPay contact and request the credit analysis of your buyers.

<br />

## Step 2: Create order

Once your customer chooses to pay with CrediPay, you should call our order creation endpoint. Conceptually, what this does is 'reserve' the credit limit of this customer. Keep in mind, the parameters passed in this endpoint should be within those returned to you in the previous step.

[More details](/reference/post-create-order)

<br />

## Step 3: Send invoice

What formalizes a business transaction is the Nota Fiscal. For us to commit to paying the amounts to the seller, we ask for the XML to be sent to us through this endpoint. If the data in the XML does not match the data of the Order, we cannot assure it will be accepted.

PS: After an invoice is sent, an order can no longer be canceled, only refunded.

[More details](/reference/post-submit-invoice-xml)