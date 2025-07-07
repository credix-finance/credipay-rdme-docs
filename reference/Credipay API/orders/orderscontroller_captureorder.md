---
title: Capturar um pedido
excerpt: >-
  Este é um endpoint assíncrono que permite o envio de um arquivo XML de Nota
  Fiscal para um pedido. Assim que o arquivo XML for enviado, um job será
  acionado para realizar validações e capturar o pedido.
api:
  file: open-api.yaml
  operationId: OrdersController_captureOrder
hidden: false
next:
  pages:
    - slug: orderscontroller_captureorder
      title: Capturar pedido
      type: endpoint
---