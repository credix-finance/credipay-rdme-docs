---
title: Glossário
excerpt: >-
  Entenda os principais termos usados neste guia e como eles se aplicam à
  jornada com a CrediPay.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
### Principais termos e conceitos

Durante esta documentação, alguns termos são utilizados de forma recorrente. Compreender o significado exato de cada um é fundamental para interpretar corretamente os fluxos e integrar com a API da CrediPay.

| Termo                        | Definição                                                                                                                                                               |
| :--------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Vendedor (Seller)            | Empresa que utiliza a CrediPay como meio de pagamento em sua operação B2B. É quem cria os pedidos e recebe os valores antecipados após a emissão da nota fiscal.        |
| Comprador (Buyer)            | Cliente do vendedor. É o responsável pelo aceite da operação de crédito e pelo pagamento das parcelas conforme o prazo definido.                                        |
| Pedido (Order)               | Representa uma solicitação de crédito no sistema da CrediPay. A criação do pedido reserva o limite de crédito do comprador até a emissão e validação da nota fiscal.    |
| Nota Fiscal (Invoice)        | Documento fiscal (NF-e) vinculado a um pedido. É enviado pelo vendedor após a confirmação do comprador e é necessário para que a operação seja liquidada.               |
| Parcelas (Repayments)        | Cada pedido pode ser dividido em uma ou mais parcelas, com valores e vencimentos definidos no momento da operação.                                                      |
| Reembolso (Refund)           | Processo de devolução parcial ou total de uma transação após emissão da nota fiscal — por exemplo, em caso de devolução de produto, erro no faturamento ou não entrega. |
| Limite de Crédito Total      | Valor máximo que um comprador pode manter em aberto com a CrediPay, considerando todas as suas operações ativas.                                                        |
| Limite de Crédito Utilizado  | Somatório dos valores vinculados a pedidos já criados e não quitados. Representa a exposição atual do comprador.                                                        |
| Limite de Crédito Disponível | Diferença entre o limite total e o limite utilizado. Representa o valor ainda disponível para novas transações.                                                         |
| Prazo de Pagamento do Pedido | Intervalo entre a data da operação e o vencimento da primeira parcela.                                                                                                  |
| Prazo Máximo de Pagamento    | Prazo limite disponível para um comprador específico, com base em sua análise de crédito.                                                                               |