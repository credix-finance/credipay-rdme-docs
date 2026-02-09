---
title: Criar um pedido por NF-e
excerpt: >-
  Permite criar um pedido enviando um arquivo XML de Nota Fiscal. Se orderId não
  for informado, um novo pedido é criado. Se orderId for informado, a nota
  fiscal é vinculada ao pedido especificado. Para que uma nota fiscal seja
  aceita, ela precisa estar dentro do limite de crédito disponível do comprador
  e do prazo máximo de pagamento.
api:
  file: open-api.yaml
  operationId: OrdersController_postInvoiceXml
hidden: false
---