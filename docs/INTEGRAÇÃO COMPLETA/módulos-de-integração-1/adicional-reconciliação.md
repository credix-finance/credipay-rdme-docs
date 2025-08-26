---
title: 'Adicional: Reconciliação'
deprecated: false
hidden: true
metadata:
  robots: index
---
# Introdução

Para facilitar o processo de reconciliação financeira dos nossos vendedores, desenvolvemos um novo endpoint na nossa API. O objetivo principal desta funcionalidade é permitir que o vendedor possa automatizar a conciliação dos pagamentos (desembolsos) que realizamos para a sua empresa.

Com os dados fornecidos, será possível conectar de forma simples e direta cada transferência recebida em sua conta bancária com as respectivas notas fiscais (NFs) e duplicatas que estão sendo liquidadas no seu sistema de gestão (ERP).

# Resposta do endpoint

Abaixo, um exemplo de resposta que será retornada ao chamar esse endpoint

```
{
  "data": [
    {
      "reference": "DESEMBOLSO-CONTRATO-XYZ123",
      "totalAmountCents": 985000,
      "disbursedAt": "2025-08-27T10:30:00.000Z",
      "payee": {
        "bankAccount": {
          "bank_identification_code": "341",
          "branch_number": "0001",
          "branch_digit": null,
          "account_number": "123456",
          "account_digit": "7"
        }
      },
      "payer": {
        "name": "CrediPay Fundo de Investimento em Direitos Creditórios Comerciaos de Responsabilidade Limitada",
        "taxId": "58211468000105",
        "bankAccount": {
          "bank_identification_code": "208",
          "branch_number": "1234",
          "branch_digit": "5",
          "account_number": "123456",
          "account_digit": "7"
        }
      },
      "transactions": [
        {
          "type": "AdvanceFaceValue",
          "amountCents": 1000000,
          "invoiceKey": "41250812345678000199550010001234561000000015",
          "invoiceNumber": "123456",
          "maturityDate": "2025-09-15",
          "duplicata": 1,
          "order_external_Id": "PEDIDO-A456"
        },
        {
          "type": "AdvanceDiscount",
          "amountCents": -10000,
          "invoiceKey": "41250812345678000199550010001234561000000015",
          "invoiceNumber": "123456",
          "maturityDate": "2025-09-15",
          "duplicata": 1,
          "order_external_Id": "PEDIDO-A456"
        },
        {
          "type": "TxFee",
          "amountCents": -5000,
          "invoiceKey": "41250812345678000199550010001234561000000015",
          "invoiceNumber": "123456",
          "maturityDate": "2025-09-15",
          "duplicata": 1,
          "order_external_Id": "PEDIDO-A456"
        }
      ]
    }
  ],
  "page": 1,
  "items": 1,
  "total": 1
}
```

## Detalhamento dos campos

<br />

| Campo     | Tipo | Descrição |
| :-------- | :--- | :-------- |
| reference |      |           |
|           |      |           |
