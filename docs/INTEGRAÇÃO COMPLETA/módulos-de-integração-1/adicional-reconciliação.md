---
title: 'Adicional: Reconciliação'
deprecated: false
hidden: false
metadata:
  robots: index
---
# Introdução

Para facilitar o processo de reconciliação financeira dos nossos vendedores, desenvolvemos um novo endpoint na nossa API. O objetivo principal desta funcionalidade é permitir que o vendedor possa automatizar a conciliação dos pagamentos (desembolsos) que realizamos para a sua empresa.

Com os dados fornecidos, será possível conectar de forma simples e direta cada transferência recebida em sua conta bancária com as respectivas notas fiscais (NFs) e duplicatas que estão sendo liquidadas no seu sistema de gestão (ERP).

Não há webhook de repasse. Consulte o endpoint por janela de datas (`startDate` é obrigatório) e use o `referenceCode` para não processar o mesmo repasse duas vezes.

# Resposta do endpoint

Abaixo, um exemplo de resposta que será retornada ao chamar esse endpoint

```json
{
  "data": [
    {
      "referenceCode": "DESEMBOLSO-CONTRATO-XYZ123",
      "totalAmountCents": 990000,
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
        "name": "CrediPay Fundo de Investimento em Direitos Creditórios Comerciais de Responsabilidade Limitada",
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
          "invoiceKey": "0123456",
          "invoiceNumber": "NFe41250812345678000199550010001234561000000015",
          "maturityDate": "2025-09-15",
          "duplicata": 1,
          "orderExternalId": "PEDIDO-A456"
        },
        {
          "type": "AdvanceDiscount",
          "amountCents": -10000,
          "invoiceKey": "0123456",
          "invoiceNumber": "NFe41250812345678000199550010001234561000000015",
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

* **referenceCode:** Identificador da transferência bancária
* **totalAmountCents:** Valor total da transferência, em centavos
* **disbursedAt:** Data da transferência
* **seller:** Dados do vendedor (destinatário da transferência)
* **payer:** Dados do pagador (originário da transferência)
* **transactions:** Transações que estão sendo pagas ou cobradas dentro desta transferência
* **type:** Tipo da transação. Os principais tipos são:
  * AdvanceFaceValue: O valor total do recebível, sobre o qual será aplicada a taxa de desconto.
  * AdvanceDiscount: O percentual deduzido no momento do desembolso, proporcional ao prazo de pagamento do recebível. Só existe na antecipação; no pagamento garantido, a duplicata não tem essa linha.
  * TxFee: Tarifa cobrada sobre o valor de face no percentual do contrato, como a do pagamento garantido.
  * Refund: Valor devolvido ao comprador. Quando a duplicata ainda não foi paga ao vendedor, entra no mesmo repasse que ela. Quando já foi paga, é descontado de um repasse seguinte.
  * RefundDiscountAdjustment: Correção no valor do reembolso com base no tempo decorrido desde o pagamento original.
* **amountCents:** Valor da transação (o somatório dos valores das transações compõe o valor da transferência). Valores positivos são os pagos ao vendedor, e negativos os cobrados.
* **invoiceKey:** Na NF-e, os 7 últimos dígitos do número da nota
* **invoiceNumber:** Chave de acesso da nota: `NFe` seguido dos 44 dígitos, na NF-e, ou `NFS` seguido dos 50 dígitos, na NFS-e
* **maturityDate:** Vencimento da parcela (duplicata)
* **duplicata:** Número da parcela (duplicata)
* **orderExternalId:** Identificador externo do pedido