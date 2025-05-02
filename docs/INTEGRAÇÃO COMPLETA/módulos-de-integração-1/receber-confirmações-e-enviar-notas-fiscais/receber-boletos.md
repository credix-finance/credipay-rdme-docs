---
title: 2.1. Recebimento de boletos
excerpt: >-
  Dependências: Módulo 1. Checar e reservar limites de crédito e Módulo 2.
  Receber confirmações e enviar Notas Fiscais
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Introdução

A emissão de boletos pode acontecer em 2 momentos: 

- Quando um XML de NF é aceito (etapa 2) 
- Quando um reembolso parcial é executado (etapa 3). 

Em ambos os casos, enviaremos webhooks **repayment.created** assim que o boleto estiver disponível. Neste webhook, traremos o URL para o PDF do boleto, o qual pode ser disponibilizado para times internos e clientes do integrador. Para mais detalhes, cheque [Webhooks](doc:api-usage-webhooks)]