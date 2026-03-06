---
title: Capturar pedido
excerpt: >-
  Este é um endpoint assíncrono que permite enviar um arquivo XML de Nota Fiscal
  para um pedido. Assim que o arquivo XML é enviado, um job será disparado para
  realizar validações e capturar o pedido.
api:
  file: open-api.yaml
  operationId: OrdersController_captureOrder
hidden: false
---