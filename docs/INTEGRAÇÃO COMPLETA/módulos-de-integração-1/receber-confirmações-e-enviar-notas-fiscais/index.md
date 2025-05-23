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

Ao criar um pedido (e reservar o limite de crédito), a CrediPay enviará automaticamente um email de confirmação para o comprador. Quando o comprador acessar o email e confirmar o pedido, nós enviaremos um webhook order.confirmed e mudaremos o status do pedido.

Sendo feito isso, a Nota Fiscal deve ser emitida e enviada em seguida (não é possível enviar uma NF antes que o pedido seja confirmado). A CrediPay somente formalizará e se comprometerá com a transação uma vez que a NF seja aceita. Para mais informações sobre os critérios de aceite, acesse \[link para POST v2/orders/`{orderId}`/capture]\[link para POST v2/orders/`{orderId}`/capture].

Quando o XML de uma NF for aceito, os boletos serão emitidos automaticamente e enviados ao comprador. Para o integrador, pode ser interessante receber esses arquivos também. Para isso, cheque [Recebimento de boletos](doc:api-usage-receber-boletos)

# Fluxo

**Legenda:**

* :green_square: Verde: Ações tomadas pelo vendedor
* :orange_square: Laranja: Ações tomadas pela CrediPay

<br />

```mermaid
flowchart TD
    subgraph s1["<b>Somente para Televendas</b>"]
        n4["CrediPay recebe confirmacao do pedido por parte do comprador"]
        n5["Altera status do pedido"]
        n7["Envia webhook order.confirmed"]
        n6["Vendedor recebe webhook order.confirmed"]
    end
    n4 --> n5
    n5 --> n7
    n7 -- "order.confirmed" --> n6
    n6 --> n8["Vendedor emite NF"]
    n8 --> n9["Recebe aprovacao da SEFAZ na NF"]
    n9 --> n10["Envia XML da NF para CrediPay"]
    n10 -- POST v2/orders/{orderId}/capture --> n11["Recebe XML da NF"]
    n11 --> n12{"XML aprovado?"}
    n12 -- "Nao - webhook order.validationFailed" --> n13["Recebe feedback e ajusta XML"]
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

<Image align="center" className="border" border={true} width="300px" src="https://files.readme.io/37c0da471f3ed0ef38ac9063ed2b2f7d41122e2cd676471451111942d2549087-Editor___Mermaid_Chart-2025-04-25-194833.png" />