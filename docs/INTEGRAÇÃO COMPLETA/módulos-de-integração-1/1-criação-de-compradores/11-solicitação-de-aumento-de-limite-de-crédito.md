---
title: 1.1 Solicitação de Aumento de Limite de Crédito
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