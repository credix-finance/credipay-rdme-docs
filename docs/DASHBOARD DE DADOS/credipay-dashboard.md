---
title: Seções do dashboard
excerpt: O CrediPay Dashboard é a central de acompanhamento das suas operações.
deprecated: false
hidden: false
metadata:
  robots: index
---
Ele consolida em um único lugar as informações de desembolsos, limites de crédito e pedidos em aberto — atualizadas automaticamente e filtradas para a sua empresa.

## Seções do dashboard

### Reconciliação de Desembolsos

Esta seção apresenta um detalhamento completo de todos os valores pagos e cobrados pela CrediPay em cada desembolso.

Cada desembolso é composto por uma ou mais transações, que aparecem como linhas na tabela. Os principais tipos de transação são:

| Tipo                    | Descrição                                                                    |
| ----------------------- | ---------------------------------------------------------------------------- |
| **Valor de Face**       | Valor total do recebível antecipado                                          |
| **Taxa de Desconto**    | Percentual deduzido no momento do desembolso, proporcional ao prazo          |
| **Reembolso**           | Ajuste quando há devolução por parte do comprador                            |
| **Ajuste de Reembolso** | Correção do reembolso com base no tempo decorrido desde o pagamento original |
| **Coobrigação**         | Valor cobrado em caso de inadimplência do comprador (recourse)               |
| **Repagamento**         | Valor recebido após cobrança de coobrigação                                  |

> Valores **positivos** são pagados pela CrediPay; valores **negativos** são cobrados pela CrediPay.

**Como localizar uma transferência no extrato bancário:** use o campo **Referência** para encontrar o PIX ou TED correspondente.

**Sobre o remetente do pagamento:** os valores podem ser transferidos por duas entidades diferentes:

- _Credix Finance Securitizadora III S.A._ — todas as transações do dia são agrupadas em um único pagamento.
- _CrediPay FIDC_ — cada recebível é pago separadamente, gerando transferências individuais.

#### Indicadores do período

Os cartões no topo da seção resumem o período selecionado:

- **Valor total desembolsado** — soma de todos os valores pagos no período
- **Número de desembolsos** — quantidade de grupos de transferência realizados
- **Ticket médio** — valor médio por desembolso
- **Total face value** — soma dos valores de face antecipados
- **Total desconto** — soma das taxas de desconto cobradas
- **Total reembolso** — soma dos valores devolvidos
- **NFs únicas** — quantidade de notas fiscais distintas no período
- **Pedidos únicos** — quantidade de pedidos distintos no período

#### Desembolsos Agendados

Tabela com os desembolsos previstos para datas futuras. Permite antecipar o fluxo de caixa esperado com base nos recebíveis já capturados.

#### Desembolsos por Pedido

Matriz cruzando data de criação do pedido com data de desembolso, mostrando o volume e o tempo entre a criação do pedido e o efetivo pagamento.

***

### Limites de Crédito

Esta seção apresenta os limites de crédito aprovados, o consumo atual e a disponibilidade de cada comprador cadastrado na plataforma.

| Coluna                     | Descrição                                                     |
| -------------------------- | ------------------------------------------------------------- |
| **Nome Comprador**         | Razão social do grupo econômico                               |
| **CNPJ**                   | CNPJ da matriz do grupo econômico                             |
| **Limite Total (R$)**      | Valor total aprovado pela CrediPay para este comprador        |
| **Limite Disponível (R$)** | Quanto do limite ainda pode ser utilizado (Total − Consumido) |
| **Filiais (CNPJs)**        | Demais CNPJs do mesmo grupo econômico                         |

> Um comprador aparece como **sem limite** quando ainda não passou pela análise de crédito ou quando foi considerado inelegível.

A seção também exibe uma **segmentação por faixa de limite**, separando compradores em:

- **Ativos** — realizaram algum pedido nos últimos 90 dias
- **Inativos** — elegíveis com limite disponível, mas sem pedido recente

***

### Acompanhamento de Pedidos

Esta seção monitora pedidos que ainda não foram concluídos.

| Status                     | Descrição                                              |
| -------------------------- | ------------------------------------------------------ |
| **Aguardando confirmação** | Pedido criado, mas ainda não confirmado pelo comprador |
| **NF-e necessária**        | Pedido confirmado, aguardando envio da nota fiscal     |

Use esta seção para identificar pedidos travados e acionar o comprador ou o time de suporte CrediPay conforme necessário.

***

## Dúvidas e suporte

- **Documentação completa:** [docs.credipay.credix.finance](https://docs.credipay.credix.finance)
- **Reconciliação de desembolsos:** [docs.credipay.credix.finance/docs/reconciliação-de-desembolsos](https://docs.credipay.credix.finance/docs/reconciliação-de-desembolsos)
- Para suporte, entre em contato com o time CrediPay pelo canal habitual.

<br />
