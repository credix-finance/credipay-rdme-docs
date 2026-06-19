---
title: Cancelamentos & reembolsos
deprecated: false
hidden: true
metadata:
  robots: index
---
Funciona pelo mesmo caminho do faturamento: a CrediPay recebe automaticamente os reembolsos e cancelamentos da VTEX, que por sua vez os recebe do ERP — sem nenhuma ação manual.

Quando isso acontece:

* **Boletos ajustados** — os boletos em aberto do comprador são ajustados ou cancelados para refletir o novo valor, garantindo uma cobrança coerente.
* **Limite recomposto** — o valor reembolsado volta ao limite disponível do comprador, liberando-o para novas compras.
* **Sem transferência** — você não precisa nos transferir o valor reembolsado. Ele é descontado do seu próximo adiantamento. Esse detalhamento está na página de Relatórios.

**Como isso se integra ao ERP?**

Com a integração ERP ↔ VTEX configurada, não é necessário nenhum ajuste adicional: reembolsos e cancelamentos fluem automaticamente para a VTEX e, em seguida, para a CrediPay.

> 🚧 Origem do pedido
>
> Por segurança, nunca acataremos uma solicitação de reembolso ou cancelamento vinda diretamente do comprador. Nesses casos, o vendedor é quem deve nos informar o pedido e o valor a ser reembolsado.
