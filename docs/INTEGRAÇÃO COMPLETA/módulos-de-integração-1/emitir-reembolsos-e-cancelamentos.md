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

Vale ressaltar que o endpoint **POST v2/orders/{orderId}/refund** é assíncrono. Assim que os processos de reembolso forem executados, será enviado um webhook repayment.cancelled confirmando o reembolso. Em caso de reembolsos parciais, pode ser interessante receber os novos boletos - para isso, cheque a página [2.1. Recebimento de boletos]

# Fluxo

Legenda:

- :green_square: Verde: Ações tomadas pelo vendedor
- :orange_square: Laranja: Ações tomadas pela CrediPay

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/814ccada8fef6c5d2db9f8164a3be05ed182b8557e94ae94251aefc7d76ba6c6-Editor___Mermaid_Chart-2025-04-25-200612.png",
        "",
        ""
      ],
      "align": "center",
      "sizing": "350px",
      "border": true
    }
  ]
}
[/block]