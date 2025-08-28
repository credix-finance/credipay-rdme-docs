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
      "seller": {
        "bankAccount": {
          "bankIdentificationCode": "341",
          "branchNumber": "0001",
          "branchDigit": null,
          "accountNumber": "123456",
          "accountDigit": "7"
        }
      },
      "payer": {
        "name": "CrediPay Fundo de Investimento em Direitos Creditórios Comerciaos de Responsabilidade Limitada",
        "taxId": "58211468000105",
        "bankAccount": {
          "bankIdentificationCode": "208",
          "branchNumber": "1234",
          "branchDigit": "5",
          "accountNumber": "123456",
          "accountDigit": "7"
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
          "orderExternalId": "PEDIDO-A456"
        },
        {
          "type": "AdvanceDiscount",
          "amountCents": -10000,
          "invoiceKey": "41250812345678000199550010001234561000000015",
          "invoiceNumber": "123456",
          "maturityDate": "2025-09-15",
          "duplicata": 1,
          "orderExternalId": "PEDIDO-A456"
        },
        {
          "type": "TxFee",
          "amountCents": -5000,
          "invoiceKey": "41250812345678000199550010001234561000000015",
          "invoiceNumber": "123456",
          "maturityDate": "2025-09-15",
          "duplicata": 1,
          "orderExternalId": "PEDIDO-A456"
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

Abaixo, um descritivo dos campos presentes no objeto da resposta:

* **reference:** Identificador da transferência bancária
* **totalAmountCents:** Valor total da transferência, em centavos
* **disbursedAt:** Data da transferência
* **seller:** Dados do vendedor (destinatário da transferência)
* **payer:** Dados do pagador (originário da transferência)
* **transactions:** Transações que estão sendo pagas ou cobradas dentro desta transferência
* **type:** Tipo da transação. Os principais tipos são:
  * AdvanceFaceValue: O valor total do recebível, sobre o qual será aplicada a taxa de desconto.
  * AdvanceDiscount: O percentual deduzido no momento do desembolso, proporcional ao prazo de pagamento do recebível.
  * Refund: Se houver um pedido de reembolso por parte do comprador, a CrediPay ajustará os boletos já pagos e descontará esse valor do próximo desembolso.
  * RefundDiscountAdjustment: Correção no valor do reembolso com base no tempo decorrido desde o pagamento original.
* **amountCents:** Valor da transação (o somatório dos valores das transações compõe o valor da transferência)
* **invoiceKey:** Chave de 44 dígitos da Nota Fiscal
* **invoiceNumber:** Número da Nota Fiscal
* **maturityDate:** Vencimento da parcela (duplicata)
* **duplicata:** Número da parcela (duplicata)
* **orderExternalId:** Identificador externo do pedido
