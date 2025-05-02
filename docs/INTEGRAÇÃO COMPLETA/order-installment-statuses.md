---
title: Guia de Status
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
O funcionamento do CrediPay é baseado em dois conceitos principais: **Pedidos (Orders)** e **Parcelas (Repayments)**.

- **Orders** representam a reserva de uma parte do limite de crédito do comprador, que posteriormente é formalizada quando há o aceite do comprador e o envio da Nota Fiscal (NF).
- **Repayments** são geradas automaticamente após o envio da NF. Cada parcela corresponde a um valor com uma data de vencimento definida.

***

## Status de Pedido (Order)

| Status                | Descrição                                                                                                                       |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Created**           | Ordem criada com sucesso, aguardando aceitação do cliente via e-mail.                                                           |
| **WaitingInvoice**    | Aguardando o envio do XML da nota fiscal após a aceitação da ordem. Ao utilizar a v2/orders/invoice, o pedido pula esse status. |
| **Captured**          | Ordem concluída com sucesso, com todos os passos finalizados.                                                                   |
| **ValidationFailed**  | Validação da nota fiscal falhou; é possível reenviar para nova tentativa.                                                       |
| **Cancelled**         | Ordem cancelada por ação do cliente (antes do envio da NF).                                                                     |
| **PartiallyRefunded** | Parte do valor do pedido foi estornado após o envio da NF.                                                                      |
| **FullyRefunded**     | Valor total do pedido foi estornado após o envio da NF.                                                                         |

***

## Status de Cobrança (Repayment)

| Status                | Descrição                                                                              |
| --------------------- | -------------------------------------------------------------------------------------- |
| **Open**              | Parcela criada, aguardando pagamento.                                                  |
| **ProcessingPayment** | Pagamento em processamento bancário. O limite de crédito do comprador já foi liberado. |
| **Paid**              | Pagamento confirmado e parcela quitada.                                                |
| **Canceled**          | Parcela cancelada, geralmente por substituição por outras.                             |
| **Failed**            | Falha na criação da parcela.                                                           |