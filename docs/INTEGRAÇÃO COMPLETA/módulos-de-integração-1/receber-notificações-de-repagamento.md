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
    n4["CrediPay recebe a notificação do pagamento do pedido"] --> n5{"Pago via boleto ou pix?"}
    n5 -- Boleto --> n6["Recebe notificacao de pagamento em processamento"]
    n5 -- Pix --> n9["Valor compensado na conta bancária"]
    n6 --> n7["Envia webhook repayment.processing"]
    n7 -- "repayment.processing" --> n12["Vendedor recebe webhook repayment.processing"]
    n7 --> n8["Libera limite de crédito"]
    n8 --> n9
    n9 -- Pix --> n11["Libera limite de crédito"]
    n10["Envia webhook repayment.settled"] -- "repayment.settled" --> n13["Vendedor recebe webhook repayment.settled"]
    n9 --> n10
    n12 --> n14@{ label: "Marca como 'em processamento'" }
    n13 --> n15@{ label: "Marca como 'pago'" }

    n14@{ shape: rect }
    n15@{ shape: rect }

    n4:::credipay
    n5:::credipay
    n6:::credipay
    n9:::credipay
    n7:::credipay
    n12:::vendedor
    n8:::credipay
    n11:::credipay
    n10:::credipay
    n13:::vendedor
    n14:::vendedor
    n15:::vendedor

    classDef vendedor fill:#C6F7D0,stroke:#333,stroke-width:1px,color:#000;
    classDef credipay fill:#FFD8A8,stroke:#333,stroke-width:1px,color:#000;

```