---
title: Cancelamentos & reembolsos
deprecated: false
hidden: false
metadata:
  robots: index
---
Funciona pelo mesmo caminho do faturamento: a CrediPay recebe automaticamente os reembolsos e cancelamentos da VTEX, que por sua vez os recebe do ERP, sem nenhuma ação manual.

O que muda é **quando** o cancelamento acontece: antes ou depois da nota fiscal. Esse é o divisor de águas, porque é a nota que dispara o fluxo financeiro.

## Antes da nota fiscal

***

O caso mais simples. O pedido ainda está aberto, a nota não foi faturada e a CrediPay ainda não desembolsou nada.

Basta cancelar o pedido. A CrediPay libera a reserva e o limite do comprador volta a ficar disponível. Não há acerto financeiro a fazer.

## Depois da nota fiscal

***

Nesse momento a CrediPay já executou o fluxo financeiro: recebeu a nota, emitiu o boleto para o comprador e desembolsou o valor para o vendedor.

### Cancelamento ou reembolso total

Três coisas acontecem ao mesmo tempo:

* **Boletos cancelados** — os boletos em aberto do comprador são cancelados.
* **Limite recomposto** — o valor volta ao limite disponível do comprador, liberando-o para novas compras.
* **Sem transferência** — você não precisa nos transferir o valor reembolsado. Como já desembolsamos, ele é retido no seu próximo adiantamento. Esse detalhamento está na página de Relatórios.

O ajuste acontece na conciliação financeira do repasse seguinte, o vendedor não devolve dinheiro manualmente.

<Callout icon="📘" theme="info">
  ### O que exatamente é retido

  A retenção considera o valor desembolsado mais a taxa proporcional ao período em que o vendedor esteve com o recurso, da data do desembolso até a data do reembolso. Consulte o time da CrediPay para o cálculo aplicável ao seu contrato.
</Callout>

### Reembolso parcial

O pedido continua aberto. A CrediPay **reajusta os boletos** emitidos ou em aberto para refletir o novo valor do pedido, e o limite do comprador é liberado apenas na proporção reembolsada.

O acerto no repasse segue a mesma lógica do reembolso total, aplicada sobre o valor parcial.

## Como isso se integra ao ERP

***

Com a integração ERP ↔ VTEX configurada, não é necessário nenhum ajuste adicional: reembolsos e cancelamentos fluem automaticamente para a VTEX e, em seguida, para a CrediPay.

Duas permissões precisam estar no perfil de acesso da CrediPay para que isso funcione:

* **Notify refund** — sem ela, a CrediPay não sabe que precisa reverter o ativo.
* **Cancel order** — sem ela, cancelamentos anteriores à NF não liberam a reserva de limite.

Veja [Chave de aplicação e permissões](/project/credix-credipay/v2.1/docs/chave-de-aplicação-e-permissões).

<Callout icon="🚧" theme="warn">
  ### Origem do pedido

  Por segurança, nunca acataremos uma solicitação de reembolso ou cancelamento vinda diretamente do comprador. Nesses casos, o vendedor é quem deve nos informar o pedido e o valor a ser reembolsado.
</Callout>
