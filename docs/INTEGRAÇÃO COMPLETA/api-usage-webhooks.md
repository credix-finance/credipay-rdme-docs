---
title: Webhooks
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
Os webhooks permitem que sua aplicação receba notificações em tempo real sobre eventos importantes na CrediPay, como confirmações de pedidos, criação de boletos ou pagamentos realizados.

***

## Como funcionam?

* **Formato**: Cada webhook é uma requisição `POST` enviada para o seu endpoint configurado.
* **Resposta esperada**: Responda com um código HTTP `2xx` em até 15 segundos para confirmar o recebimento.
* **Segurança**: Verifique a assinatura (signature) e o timestamp do payload para garantir a autenticidade.
* **CSRF**: Desative a proteção CSRF para esse endpoint, se estiver habilitada no seu framework.

***

## Eventos disponíveis

| Evento                   | Quando é disparado                                                                                       |
| :----------------------- | :------------------------------------------------------------------------------------------------------- |
| `order.accepted`         | Quando um pedido é confirmado pelo comprador                                                             |
| `order.rejected`         | Quando um pedido é rejeitado pelo comprador                                                              |
| `order.captured`         | Quando um XML é aceito                                                                                   |
| `order.validationFailed` | Quando um XML é recusado. Ao receber este evento, é possível enviar novas tentativas para o mesmo pedido |
| `repayment.created`      | Quando um novo boleto é criado (NF enviada, reembolso feito ou renegociação)                             |
| `repayment.settled`      | Quando um pagamento é compensado ou um reembolso total é concluído                                       |
| `repayment.cancelled`    | Quando um boleto é cancelado                                                                             |

***

## Estrutura do payload

Cada evento possui um payload em JSON com informações específicas. Para ver os esquemas e exemplos:

👉 [Catálogo de Eventos](https://app.credipay.credix.finance/webhooks/)

***

## Como adicionar um endpoint

1. Acesse a aba Webhooks no Portal do Vendedor. Se você ainda não possui uma conta, veja [Criando sua conta no portal do vendedor](/project/credix-credipay/v2.1/docs/setting-up-the-platform)
2. Informe a URL que receberá os webhooks.
3. Selecione os eventos que deseja receber (ou deixe em branco para receber todos).

***

<br />

## Estrutura do payload

Cada evento possui um payload em JSON com informações específicas. Para ver os esquemas e exemplos:

👉 [Catálogo de Eventos](🔗)

***

<br />

## Testando seu endpoint

1. Vá até a aba "Testing" no painel.
2. Envie um evento de teste.
3. Verifique o payload e a resposta.
4. Confirme se seu sistema está lidando corretamente com os dados.

***

## Verificação de assinatura

Todos os webhooks incluem cabeçalhos com assinatura para validação. Use uma biblioteca como `Svix` para validar a autenticidade.

Exemplo em JavaScript:

```javascript
import { Webhook } from "svix";

const secret = "whsec_SUA_CHAVE_SECRETA";
const headers = {
  "svix-id": "msg_ID",
  "svix-timestamp": "1614265330",
  "svix-signature": "v1,SUA_ASSINATURA",
};
const payload = '{"exemplo": "dado"}';

const wh = new Webhook(secret);
try {
  const verified = wh.verify(payload, headers);
  console.log("Payload verificado:", verified);
} catch (err) {
  console.error("Falha na verificação:", err);
}

 
```

<br />

## Tentativas e Reenvio

Se sua aplicação não responder corretamente ao webhook, a CrediPay seguirá um plano automático de retentativas com **backoff exponencial**.

<br />

### Cronograma de retentativas

| Tentativa | Intervalo       |
| --------- | --------------- |
| 1         | Imediatamente   |
| 2         | 5 segundos      |
| 3         | 5 minutos       |
| 4         | 30 minutos      |
| 5         | 2 horas         |
| 6         | 5 horas         |
| 7         | 10 horas        |
| 8+        | A cada 10 horas |

<br />

### Reenvio manual

Você pode reenviar eventos manualmente no painel da aplicação:

1. Acesse a aba de Webhooks.
2. Selecione a mensagem que falhou.
3. Clique em **"Reenviar"**.

<br />

***

<br />

## Recuperação de falhas e reenvio em lote

### Reativar endpoints

Endpoints que falharem por mais de 5 dias serão automaticamente desativados. Você pode reativá-los diretamente pelo painel da CrediPay.

### Reenvio em lote via API

Use o endpoint abaixo para reenviar todos os webhooks que falharam para um endpoint específico:

```http
POST /webhook-events/endpoints/:endpointId/recover
```
