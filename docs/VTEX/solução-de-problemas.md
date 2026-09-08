---
title: Solução de Problemas
deprecated: false
hidden: false
metadata:
  robots: index
---
Boa parte dos problemas de integração VTEX vem de uma configuração faltando, não de uma falha. Abaixo, os sintomas mais frequentes, a causa provável de cada um e como corrigir.

## Checkout

***

### "Boleto a prazo" não aparece no checkout

Verifique, nesta ordem:

* **A condição de pagamento existe e está ativa** — em Configurações de pagamento → Condições.
* **Já se passaram 10 minutos desde que você salvou** — a VTEX leva até 10 min para propagar.
* **O provedor CrediPay está salvo com App Key e App Token corretos** — veja [Provedor e meio de pagamento](/project/credix-credipay/v2.1/docs/provedor-e-meio-de-pagamento).
* **O comprador tem limite disponível** — consulte o CNPJ no dashboard da CrediPay.

### O comprador seleciona CrediPay e a compra falha

Causa mais provável: **o nome do meio de pagamento não confere**.

O conector aceita exatamente quatro nomes, com diferenciação de maiúsculas: `CrediPay`, `Boleto a prazo`, `Boleto a Prazo` e `Boleto a prazo CrediPay`. Qualquer outro nome faz o pagamento ser recusado.

Verifique o nome do pagamento customizado, inclusive espaços extras no fim.

### As parcelas não aparecem, só "à vista"

A etapa de habilitação das parcelas não foi executada, ou foi executada com um dos IDs errado. Confira os valores de `affiliationId`, `paymentSystemId` e `ruleId` usados na chamada, contra os IDs que aparecem nas URLs do Admin VTEX.

### As parcelas aparecem, mas sem datas de vencimento

A [interface personalizada de checkout](/project/credix-credipay/v2.1/docs/instalação-dos-apps) não está instalada ou a personalização não foi ativada. Verifique se `vtex.checkout-ui-custom` está instalado e se o script na aba JS está ativo.

## Nota fiscal e desembolso

***

### O pedido foi feito, mas o desembolso não aconteceu

O gatilho do desembolso é a **NF-e**, não o pedido. Sem nota, o limite do comprador fica reservado e o vendedor não recebe.

* **A nota foi emitida e registrada na VTEX** — confira no Admin VTEX, no pedido, na aba de notas.
* **A permissão Notify invoice está no perfil CrediPay** — veja [Chave de aplicação e permissões](/project/credix-credipay/v2.1/docs/chave-de-aplicação-e-permissões).
* **O&#x20;**`invoiceUrl`**&#x20;é público e termina em&#x20;**`.xml` — abra a URL em uma janela anônima. Se pedir login, a CrediPay não consegue ler.
* **O XML contém a tag&#x20;**`nfeProc` — XML de pré-autorização é recusado.

Pedidos aguardando nota aparecem nos [Relatórios](/project/credix-credipay/v2.1/docs/relatórios).

### A nota foi enviada mas recusada na validação

* **Número de duplicatas (**`dup`**) diferente do número de parcelas do pedido** — refature com uma duplicata por parcela.
* **Valores ou vencimentos das duplicatas não batem com o pedido** — confira contra o parcelamento escolhido no checkout.
* **Falta a tag&#x20;**`nfeProc` — envie o XML autorizado pela SEFAZ, não o de pré-autorização.
* **CNPJ do emitente não cadastrado na CrediPay** — solicite o cadastro do CNPJ ao time da CrediPay.

### O comprador recebeu dois boletos

O ERP está emitindo boleto além da CrediPay. Configure no ERP um meio de pagamento específico para a CrediPay que **não gere cobrança**. Veja [Configuração da integração](/project/credix-credipay/v2.1/docs/configuração-da-integração).

## Cancelamento e reembolso

***

### Cancelei o pedido e o limite do comprador não voltou

Verifique se as permissões **Cancel order** e **Notify refund** estão no perfil CrediPay. Sem elas, a VTEX não notifica a CrediPay e a reserva de limite permanece.

### O comprador pediu reembolso direto para a CrediPay

A CrediPay não processa reembolso solicitado pelo comprador. O pedido precisa partir do vendedor, informando o pedido e o valor. Veja [Cancelamentos & reembolsos](/project/credix-credipay/v2.1/docs/cancelamentos-reembolsos).

## Ainda com problema?

***

Ao acionar o time da CrediPay, envie:

* **Account name** da loja
* **ID do pedido** na VTEX
* **CNPJ do comprador**
* Data e hora aproximadas da ocorrência
* Print da tela ou mensagem de erro
