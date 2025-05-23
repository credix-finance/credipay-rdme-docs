---
title: 3. Pagamento de pedido
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

Sempre que um comprador pagar a CrediPay, comunicação será toda feita via webhooks. São 2 tipos:

* **repayment.processing**: Enviado assim que o comprador paga o boleto (não se aplica a Pix), mesmo que os valores não tenham sido compensados ainda.
* **repayment.settled**: Enviado assim que os valores são compensados em nossa conta bancária.

Para fins de liberação de limite de crédito, usamos o momento do repayment.processing, assim conseguimos habilitar compradores a transacionar novamente assim que realizam o pagamento.

IMPORTANTE: **Todas** as cobranças da CrediPay são feitas via BolePix, ou seja, os compradores têm a opção de pagar tanto por boleto, quanto por Pix.

# Fluxo

**Legenda:**

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