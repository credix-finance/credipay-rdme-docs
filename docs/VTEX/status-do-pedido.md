---
title: Status do pedido
excerpt: >-
  Cada pedido passa por estados previsíveis. Use esta referência para saber o
  que cada status significa e o que fazer.
deprecated: false
hidden: true
metadata:
  robots: index
---
| Status | O que significa | O que fazer |
| --- | --- | --- |
| **Aguardando confirmação** | O comprador iniciou o pagamento e precisa confirmar com o código de verificação (OTP). | Nada — aguarde a confirmação. Se expirar, o pedido é cancelado e o limite liberado. |
| **Pedido criado** | Pagamento confirmado. O pedido existe na VTEX e na CrediPay, e o limite do comprador foi reservado. | Separe e despache a mercadoria normalmente. |
| **Aguardando nota fiscal** | O pedido está aprovado e esperando o XML da NF-e para liberar o desembolso. | Emita a NF-e com as duplicatas corretas e deixe-a fluir pela VTEX. |
| **Validando nota** | A CrediPay recebeu o XML e está validando estrutura, duplicatas e endereço. | Aguarde. Em caso de erro, o status muda para "NF recusada". |
| **Faturado** | NF-e validada e recebível registrado. O desembolso é disparado (até 24h úteis). | Nada — o valor está a caminho da sua conta. |
| **Faturado parcialmente** | Parte do pedido foi faturada (entrega faseada). O restante segue aguardando NF-e. | Emita as notas restantes para completar a captura. |
| **NF recusada** | O XML não passou na validação — em geral, falta de `nfeProc`, duplicatas divergentes ou `invoiceUrl` inacessível. | Corrija a NF-e no ERP e reenvie. Consulte os detalhes do erro com o suporte. |
| **Recusado / Expirado** | O comprador não foi aprovado, ou o pedido expirou sem confirmação/NF-e. | O limite reservado é liberado automaticamente. Nenhuma ação necessária. |
| **Reembolsado** | O pedido foi reembolsado total ou parcialmente. Boletos ajustados e limite recomposto. | Nada — veja a página de Cancelamentos & reembolsos para o impacto financeiro. |

> 📘 Caminho feliz
>
> Pedido criado → Aguardando nota fiscal → Validando nota → **Faturado**. A partir do faturamento, o desembolso acontece em até 24h úteis.
