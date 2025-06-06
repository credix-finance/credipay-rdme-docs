---
title: 'Adicional: Solicitação de Aumento de Limite de Crédito'
deprecated: false
hidden: false
metadata:
  robots: index
---
## Enviar Solicitação

**POST** `/v2/credit-limit/increase`

Envie uma solicitação para aumentar o limite de crédito de um comprador. A solicitação é avaliada de forma assíncrona, e seu status pode ser consultado periodicamente usando o endpoint `GET`.

**Parâmetros**

```json
{
  "buyerTaxId": "51137104000183",
  "sellerTaxId": "51137104000110",
  "creditLimitRequestedCents": 1000
}
```

**Exemplo de Resposta**

```json
{
  "id": "8a918d24-b0b8-4500-aadd-044b91911123",
  "buyerTaxId": "51137104000183",
  "sellerTaxId": "51137104000110",
  "creditLimitRequestedCents": 1000,
  "creditLimitApprovedCents": null,
  "status": "Created",
  "reason": null
}
```

***

## Consultar Solicitação

Para buscar o resultado da análise, é possível usar o webhook `credit-limit.increase.finished` ou o endpoint GET `/v2/credit-limit/increase/{cl_increase_request_id}`. Veja mais detalhes abaixo.

**Webhook** `credit-limit.increase.finished`

Assim que a análise for finalizada, enviaremos este webhook.

**Exemplo de Webhook**

```json json
{
    "notificationType": "credit-limit.increase.finished",
    "notificationData": {
        "organization": {
            "id": "seller-org-id"
        },
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "status": "Finished",
        "reason": null,
        "buyerTaxId": "12345678901234",
        "sellerTaxId": "98765432109876"
        "credit_limit_requested_cents": 1000
        "credit_limit_approved_cents": 10000
    }
}
```

<br />

**GET** `/v2/credit-limit/increase/{cl_increase_request_id}`

**Exemplo de Resposta**

```json
{
  "id": "8a918d24-b0b8-4500-aadd-044b91911123",
  "buyerTaxId": "51137104000183",
  "sellerTaxId": "51137104000110",
  "creditLimitRequestedCents": 1000,
  "creditLimitApprovedCents": 800,
  "status": "Rejected",
  "reason": "Comprador não elegível para um aumento de limite no momento"
}
```

***

## Guia de Status da Solicitação de Aumento de Limite

| Status            | Descrição                                                                 |
| ----------------- | ------------------------------------------------------------------------- |
| Created           | A solicitação foi recebida, mas ainda não foi processada.                 |
| Pending           | A solicitação está atualmente em avaliação.                               |
| Approved          | O valor total solicitado foi aprovado.                                    |
| PartiallyApproved | Um limite inferior ao solicitado foi aprovado.                            |
| Rejected          | A solicitação foi negada (consulte o campo `reason` para mais detalhes).  |
| Failed            | O processo de avaliação falhou devido a erros de sistema ou de validação. |