---
title: 1. Criação de pedido
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

A primeira etapa da integração é o de checagem e reserva de limites de crédito. Com ele, um integrador pode consultar as condições de pagamento de um comprador (`GET v2/buyers?taxId={CNPJ}`) com a CrediPay, e assim saber como ofertá-las a seus clientes.

Caso uma venda seja concretizada, o integrador pode realizar a reserva do limite de crédito ao criar um pedido (`POST v2/orders`). Um retorno de sucesso neste endpoint significa que a CrediPay aceitou o pedido, reservou o limite, e enviou o email de confirmação para o comprador.

> 💡 **IMPORTANTE**
>
> A CrediPay se comprometerá a pagar o pedido ao vendedor uma vez que o mesmo tenha sido confirmado pelo comprador, e uma NF tenha sido enviada e aceita - ver abaixo.

# Fluxos

**Legenda:**

* :blue_square: Azul: Ações tomadas pelo comprador
* :green_square: Verde: Ações tomadas pelo vendedor
* :orange_square: Laranja: Ações tomadas pela CrediPay

## E-commerce

<br />

```mermaid
flowchart TD
    n4["Comprador entra na página de checkout"] --> n5["Vendedor chama API da CrediPay<br>GET v2/buyers?taxId={CNPJ}<br>"]
    n6["Credipay recebe chamada"] --> n7["Retorna dados do comprador (limite de crédito, eligibilidade, prazo de pagamento, status de cadastro)"]
    n8["Vendedor recebe dados do comprador"] --> n9{"Pedido está dentro das condições de pagamento?"}
    n9 -- Não --> n10["Comprador não deve ver opção de pagamento com CrediPay"]
    n9 -- Sim --> n18["Comprador vai ver a opção de pagar com CrediPay"]
    n18 --> n19{"Escolheu CrediPay como forma de pagamento?"}
    n19 -- Sim --> n11["Vendedor envia pedido para CrediPay"]
    n19 -- Não --> n20["Pedido não será enviado para CrediPay"]
    n11 -- POST v2/orders --> n12["CrediPay recebe pedido"]
    n12 --> n13{"Pedido aceito?"}
    n13 -- Não – Retorno 4XX --> n14["Vendedor não deve criar pedido"]
    n13 -- Sim --> n15["Reserva limite de crédito"]
    n15 --> n16["Retorna pedido"]
    n16 -- Sim – Retorno 200 --> n17["Vendedor salva pedido com o orderId da CrediPay"]
    n7 --> n8
    n5 --> n6

    n4:::vendedor
    n5:::comprador
    n6:::credipay
    n7:::credipay
    n8:::comprador
    n9:::comprador
    n10:::vendedor
    n18:::vendedor
    n19:::vendedor
    n11:::comprador
    n20:::vendedor
    n12:::credipay
    n13:::credipay
    n14:::comprador
    n15:::credipay
    n16:::credipay
    n17:::comprador

    classDef vendedor fill:#AEDFF7,stroke:#333,stroke-width:1px,color:#000;
    classDef comprador fill:#C6F7D0,stroke:#333,stroke-width:1px,color:#000;
    classDef credipay fill:#FFD8A8,stroke:#333,stroke-width:1px,color:#000;

```

<Image align="center" src="https://files.readme.io/b93bf3cdc6cd771924a19ad9c7dafa2ad1d5489adb31438789332676fa8d4756-Untitled_diagram-2025-04-25-192911.png" />

## Televendas

<Image align="center" src="https://files.readme.io/70df0be34088968a0897d0e5f513daee3549a735241a7f2e79a6ebe39f44302f-Editor___Mermaid_Chart-2025-04-25-202223.png" />