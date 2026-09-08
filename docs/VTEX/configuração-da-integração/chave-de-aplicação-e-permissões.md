---
title: Chave de Aplicação e Permissões
excerpt: 'O conector da CrediPay precisa de acesso à API da sua loja VTEX para operar. '
deprecated: false
hidden: false
metadata:
  robots: index
---
Esse acesso é concedido em duas partes: você cria um **perfil de acesso** com as permissões necessárias e adiciona a **chave da CrediPay** como chave de terceiros vinculada a esse perfil.

<Callout icon="🚧" theme="warn">
  ### Falha silenciosa

  Esta é a etapa que mais causa problema difícil de diagnosticar. Faltando uma permissão, a compra pode até acontecer, mas um passo posterior do fluxo (nota fiscal, reembolso, cancelamento) para de funcionar **sem mensagem de erro**.
</Callout>

## 1. Criar o perfil de acesso

***

No Admin VTEX:

* Clique no seu usuário → **Configurações da conta** → **Perfis de acesso (Roles)**
* **Novo perfil** → **Customizado**
* Nome: `CrediPay`
* Em **Produtos e recursos**, marque **OMS** (todas as caixas de _OMS Access_) e **PCI Gateway** (todas as caixas)
* Salve

## 2. Adicionar a chave da CrediPay

***

Ainda em **Configurações da conta**:

* Vá em **Chaves de aplicação (Application keys)**
* Clique em **Adicionar chave de terceiros (Add 3rd party key)**
* Informe a chave da CrediPay: `vtexappkey-credixpartnerbr-MNPVEJ`
* Vincule ao perfil `CrediPay` criado acima
* Salve

## Por que cada permissão é necessária

***

O perfil concentra tudo que o conector precisa para executar o ciclo completo — do pagamento à liquidação. Abaixo, o que cada permissão faz no fluxo da CrediPay.

### OMS — Order Management System

O OMS é onde os pedidos vivem.

* **Notify payment** — recebe da VTEX a notificação de que o pagamento foi confirmado pelo comprador. É o gatilho que inicia o fluxo da CrediPay.
* **Notify invoice** — recebe a NF-e quando o vendedor fatura. É o gatilho da liquidação: sem isso, o evento de nota nunca chega e o ativo financeiro nunca é criado.
* **View order** — lê os dados do pedido (valor, parcelas, CNPJ do comprador) para validar e criar o pagamento.
* **Change order workflow status** — move o pedido para os estados corretos, por exemplo de _pagamento aprovado_ para _pronto para envio_, após a confirmação do comprador.
* **Notify refund** — recebe a notificação de reembolso da VTEX. Sem isso, a CrediPay não sabe que precisa reverter o ativo e devolver o limite do comprador.
* **Cancel order** — recebe cancelamentos anteriores à emissão da NF-e. Sem isso, a reserva de limite não é liberada automaticamente.
* **Change order** — atualiza dados do pedido quando necessário, como o ajuste de valor em um reembolso parcial.
* **Order feed subscription** — assina o feed de eventos de pedido, permitindo receber atualizações em tempo real sem polling.
* **Feed v3 e Hook Admin (view only)** — gerencia e recebe os webhooks de evento de pedido. É a base do fluxo assíncrono.
* **List orders** — lista pedidos para fins de conciliação e suporte.
* **View store sales stats** — leitura para conciliação e monitoramento.

### PCI Gateway

O PCI Gateway é o módulo de pagamentos da VTEX. É onde o conector vive e onde a lógica de crédito roda. Marque todas as caixas.

* **Payment-MakePayments / Process payments** — executa a transação de pagamento. Sem isso o conector não processa nenhuma compra.
* **Payment-NotifyPayments** — recebe os callbacks de status da VTEX. É o mecanismo que avisa o conector quando um pagamento é confirmado ou recusado.
* **Payment-ViewPaymentData** — lê o status da transação, necessário para o conector verificar se um pagamento foi aprovado ou negado.
* **Payment-ManageStore** — configura e gerencia as regras de pagamento da loja (condições, afiliações).
* **Payment-ManageInfrastructure** — gerencia a infraestrutura do gateway, necessário no setup e na manutenção da integração.
* **View / Edit** — permissões base de leitura e escrita no módulo de pagamentos.

## Como validar

***

Depois de salvar, confirme com o time da CrediPay antes de seguir. Um teste rápido: peça à CrediPay para consultar um pedido da sua loja pela API. Se retornar, o acesso está correto.

Próximo passo: [Provedor e meio de pagamento](/project/credix-credipay/v2.1/docs/provedor-e-meio-de-pagamento).

<br />
