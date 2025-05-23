---
title: 'Adicional: Reembolsos e cancelamentos'
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
# Introdução

Quando algo não ocorre como planejado (por exemplo, produtos danificados, extravios, desistências, etc.) com um pedido, as cobranças ao comprador deverão ser ajustadas para refletirem corretamente a realidade. Em cenários assim, o cancelamento ou o valor a ser subtraído da cobrança deve ser informado para a CrediPay, para que os boletos sejam devidamente ajustados.

Vale ressaltar que o endpoint **POST v2/orders/\{orderId}/refund** é assíncrono. Assim que os processos de reembolso forem executados, será enviado um webhook repayment.cancelled confirmando o reembolso. Em caso de reembolsos parciais, pode ser interessante receber os novos boletos - para isso, cheque a página \[2.1. Recebimento de boletos]

# Fluxo

Legenda:

* :green_square: Verde: Ações tomadas pelo vendedor
* :orange_square: Laranja: Ações tomadas pela CrediPay

<br />

```mermaid
flowchart TD
    n4["Vendedor recebe pedido de reembolso ou cancelamento"] --> n5{"Pedido já tem NF?"}
    n5 -- Sim --> n6["Emite NF Devolucao"]
    n5 -- Nao --> n7["Solicita cancelamento com a CrediPay"]
    n6 --> n10["Informa a CrediPay do reembolso"]
    n7 -- POST v2/orders/{orderId}/cancel --> n8["Credipay recebe cancelamento"]
    n8 --> n9["Cancela pedido e libera o limite de crédito"]
    n10 -- POST v2/orders/{orderId}/refund --> n11["Credipay recebe pedido de reembolso"]
    n11 --> n12["Cancela os boletos anteriores e libera o limite de crédito"]
    n12 --> n13["Envia webhooks repayment.cancelled"]
    n13 --> n14["Gera novos boletos"]
    n13 -- "repayment.cancelled" --> n15["Recebe webhooks repayment.cancelled"]
    n15 --> n17["Confirma cancelamento ou reembolso do pedido"]

    n4:::vendedor
    n5:::vendedor
    n6:::vendedor
    n7:::vendedor
    n10:::vendedor
    n8:::credipay
    n9:::credipay
    n11:::credipay
    n12:::credipay
    n13:::credipay
    n14:::credipay
    n15:::vendedor
    n17:::vendedor

    classDef vendedor fill:#C6F7D0,stroke:#333,stroke-width:1px,color:#000;
    classDef comprador fill:#C6F7D0,stroke:#333,stroke-width:1px,color:#000;
    classDef credipay fill:#FFD8A8,stroke:#333,stroke-width:1px,color:#000;

```