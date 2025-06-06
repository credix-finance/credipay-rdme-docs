---
title: 0. Criação de compradores
excerpt: >-
  Embora o endpoint ofereça praticidade, recomendamos sempre iniciar pela
  importação em massa via lista, garantindo limites mais altos logo no primeiro
  uso.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Descrição Geral

A API de Análise de Crédito oferece avaliação de crédito em tempo real e onboarding automatizado de novos compradores na plataforma da Credix. Substituindo processos manuais por um fluxo de análise totalmente automatizado, ela proporciona aos vendedores visibilidade quase imediata sobre a elegibilidade dos compradores e seus limites de crédito. Com essa integração via API, a Credix permite que seus parceiros acelerem o fluxo de negociações, reduzam a carga operacional e escalem a concessão de créd...

***

## Criar Análise de Crédito

**POST** `/v2/credit-limit/request`

Inicia a análise de crédito em tempo real e realiza automaticamente o onboarding do comprador, caso ele seja elegível, sem necessidade de configuração adicional de parâmetros.

**Request**

```json
{
  "buyerTaxId": "51137104000183",
  "sellerTaxId": "33137104000110"
}
```

**Exemplo de Resposta**

```json
{
  "id": "e08f01b6-56ae-4aa4-a23d-539596413123",
  "status": "Pending"
}
```

***

## Consultar Análise de Crédito

**GET** `/v2/credit-limit/request/:requestId`

Retorna o status de uma solicitação de análise de crédito previamente enviada, para fins de visualização pelo vendedor e uso em polling.

**Exemplo de Resposta**

```json
{
  "id": "e08f01b6-56ae-4aa4-a23d-539596413123",
  "status": "Failed",
  "reason": "Internal error while running underwriting analysis",
  "retry_after": "2025-05-24T19:30:53.044310"
}
```

***

## Guia de Status da Análise

| Status   | Descrição                                                          |
| -------- | ------------------------------------------------------------------ |
| Created  | A solicitação de análise foi recebida, mas ainda não foi iniciada. |
| Pending  | O processo de análise ou onboarding está em andamento.             |
| Finished | A solicitação de análise foi concluída com sucesso.                |
| Failed   | O fluxo de análise ou onboarding encontrou um erro.                |
| Rejected | O comprador não é elegível para análise ou onboarding.             |

***

## Códigos de Motivo (reason) e Política de Retentativa (retry policy)

| Status   | Reason                                             | Política de Retentativa |
| -------- | -------------------------------------------------- | ----------------------- |
| Failed   | Internal error while running underwriting analysis | retry in 24 hours       |
| Rejected | Buyer is not eligible for underwriting             | never                   |

Notas:

* Quando aplicável, o campo `retry_after` indica quando é apropriado tentar novamente a solicitação.
* Para status `Rejected`, a tentativa não deve ser repetida automaticamente.
* Para status `Failed`, recomenda-se nova tentativa após 24 horas, salvo orientação diferente no campo `retry_after`.