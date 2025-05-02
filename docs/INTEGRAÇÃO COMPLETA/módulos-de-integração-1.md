---
title: Etapas de integração
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: checar-e-reservar-limites-de-crédito
      title: 1. Criação de pedido
    - type: basic
      slug: receber-confirmações-e-enviar-notas-fiscais
      title: 2. Formalização de pedido
    - type: basic
      slug: receber-notificações-de-repagamento
      title: 3. Pagamento de pedido
    - type: basic
      slug: emitir-reembolsos-e-cancelamentos
      title: 4. Reembolsos e cancelamentos
---
# Introdução

Para cada uma das etapas descritas no [Ciclo de vida de um pedido](/project/credix-credipay/v2.1/docs/módulos-de-integração), temos uma etapa de integração, a ser descrita nas páginas a seguir - que também incluem a parte de reembolsos e cancelamentos. Nossa recomendação é que sejam implementadas de forma sequencial, dando que existe uma interdependência entra elas. Veja abaixo um breve descritivo de cada uma, e navegue para sua respectiva página para mais detalhes

# 1. Criação de pedido

Nesta etapa, utilizaremos o endpoint **GET v2/buyers** para buscar as condições de pagamento de um comprador, e usaremos esses dados para decidir se ele está apto a transacionar com CrediPay ou não. Em caso afirmativo, chamaremos o endpoint **POST v2/orders** para criar o pedido, assim garantindo a reserva do limite de crédito, mas ainda não a oficialização - que acontecerá na próxima etapa.

# 2. Formalização de pedido

## Confirmação de pedido

Somente para vendedores que trabalham com televendas, temos uma etapa anterior ao envio da Nota Fiscal, que é a confirmação do pedido por parte do comprador. Neste caso, enviaremos ao comprador um e-mail com os dados do pedido, e em um clique, ele poderá dar o seu 'de acordo'. Com isso, o vendedor receberá um webhook **order.confirmed**, assim concluindo esta parte, e passando para a de envio da Nota Fiscal, descrita abaixo.

## Envio da NF

A formalização de um pedido se dá quando um XML de Nota Fiscal é enviado para nós através do endpoint **POST v2/order/\{orderId}/capture**, que funciona de forma assíncrona. Desta forma, o webhook **order.captured** será enviado em seguida, assim como os webhooks **repayment.created**, que trarão os dados dos boletos. Quando isso acontece, significa que nós validamos a Nota Fiscal, e já estamos realizando todos os processos para operacionalizar o crédito.\
*\*vendedores que trabalham via e-commerce podem ir direto para esta etapa*

# 3. Pagamento de pedido

Assim que o boleto for pago pelo comprador, enviaremos um webhook **repayment.processing**, sinalizando que está em processamento bancário. Neste momento, o limite de crédito do comprador já será liberado, o possibilitando de realizar novas compras. Depois, enviaremos o webhook **repayment.settled**, onde confirmamos que os valores foram compensados em nossa conta bancária.

# 4. Reembolsos e cancelamentos

## Antes do envio da NF

Caso um pedido seja cancelado antes do envio da NF, o vendedor deverá chamar o endpoint **POST v2/order/\{orderId}/cancel**, que de forma síncrona irá cancelar o pedido e liberar o limite de crédito do cliente.

## Após o envio da NF

Caso um pedido seja cancelado (total ou parcialmente) após o envio da NF, este evento deverá ser tratado como um reembolso, dado que os valores já terão sido pagos ao vendedor. Sendo assim, o endpoint **POST v2/order/\{orderId}/refund** deve ser chamado. O mesmo funciona de forma assíncrona, portanto quando o processo de reembolso for concluído, serão enviados os webhooks **repayment.cancelled** e, caso ainda haja algo a ser cobrado, também **repayment.cancelled** com os dados dos novos boletos
