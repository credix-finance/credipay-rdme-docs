---
title: 2. Formalização de pedido
excerpt: 'Dependência: Módulo 1. Checar e reservar limites de crédito'
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

O pedido precisa estar confirmado antes de você enviar a Nota Fiscal. A confirmação acontece de um de dois jeitos, conforme a configuração comercial do vendedor com a CrediPay. Em geral, ela é automática no e-commerce e feita pelo comprador em televendas (veja [Canais de vendas](doc:canais-de-vendas)).

Para saber qual vale para um pedido, leia o campo `status` na resposta do `POST /v2/orders`:

| `status` na resposta | O que acontece | O que você faz |
| :-- | :-- | :-- |
| `Accepted` ou `WaitingForInvoice` | O pedido já está confirmado. A CrediPay não envia e-mail ao comprador. | Emita e envie a NF. |
| `Created` | A CrediPay envia um e-mail com o link de confirmação para o contato informado no pedido e para o contato cadastrado do comprador. Quando o comprador confirma, o pedido muda de status e você recebe o webhook `order.buyer.accepted`. | Espere o webhook. Depois, emita e envie a NF. |

Sendo feito isso, a Nota Fiscal deve ser emitida e enviada em seguida (não é possível enviar uma NF antes que o pedido seja confirmado). A CrediPay somente formalizará e se comprometerá com a transação uma vez que a NF seja aceita. Para mais informações sobre os critérios de aceite, acesse [POST v2/orders/`{orderId}`.](https://docs.credipay.credix.finance/reference/post-capture-order)

Quando o XML de uma NF for aceito, os boletos serão emitidos automaticamente e enviados ao comprador. Para o integrador, pode ser interessante receber esses arquivos também. Para isso, cheque [Recebimento de boletos](doc:receber-boletos)

# Fluxo

**Legenda:**

* :green_square: Verde: Ações tomadas pelo vendedor
* :orange_square: Laranja: Ações tomadas pela CrediPay

<br />

```mermaid
flowchart TD
    subgraph s1["<b>Somente quando o pedido nasce Created</b>"]
        n4["CrediPay recebe confirmacao do pedido por parte do comprador"]
        n5["Altera status do pedido"]
        n7["Envia webhook order.buyer.accepted"]
        n6["Vendedor recebe webhook order.buyer.accepted"]
    end
    n4 --> n5
    n5 --> n7
    n7 -- "order.buyer.accepted" --> n6
    n6 --> n8["Vendedor emite NF"]
    n8 --> n9["Recebe aprovacao da SEFAZ na NF"]
    n9 --> n10["Envia XML da NF para CrediPay"]
    n10 -- POST v2/orders/{orderId}/capture --> n11["Recebe XML da NF"]
    n11 --> n12{"XML aprovado?"}
    n12 -- "Nao - webhook order.validation.failed" --> n13["Recebe feedback e ajusta XML"]
    n12 -- "Sim - webhook  order.captured" --> n14["Formaliza a operacao"]
    n13 --> n10
    n14 --> n15["Gera e envia boletos"]

    n4:::credipay
    n5:::credipay
    n7:::credipay
    n6:::vendedor
    n8:::vendedor
    n9:::vendedor
    n10:::vendedor
    n11:::credipay
    n12:::credipay
    n13:::vendedor
    n14:::credipay
    n15:::credipay

    classDef vendedor fill:#C6F7D0,stroke:#333,stroke-width:1px,color:#000;
    classDef comprador fill:#C6F7D0,stroke:#333,stroke-width:1px,color:#000;
    classDef credipay fill:#FFD8A8,stroke:#333,stroke-width:1px,color:#000;
    style s1 stroke:#000000,stroke-width:2px

```