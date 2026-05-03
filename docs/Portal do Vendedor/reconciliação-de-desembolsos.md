---
title: Reconciliação de Desembolsos
excerpt: >-
  Conecte cada transferência bancária recebida da CrediPay às respectivas Notas
  Fiscais e duplicatas que a originaram, para cruzar com o seu ERP
deprecated: false
hidden: false
metadata:
  robots: index
---
## Como funciona um desembolso

Quando a CrediPay antecipa um recebível, ela realiza uma transferência bancária (TED ou PIX) para a conta do vendedor. Essa transferência é chamada de **desembolso**. Um único desembolso pode consolidar múltiplas Notas Fiscais e duplicatas, dependendo da entidade pagadora.

***

## Passo a passo da reconciliação

**1. Identifique o desembolso no extrato** Use o campo **Referencia** — ele aparece na descrição da TED/PIX no seu extrato bancário.

**2. Localize a Nota Fiscal** Use o campo **Chave NF** (chave de acesso de 44 dígitos) ou o **Numero NF** (número sequencial da NF).

**3. Cruze com o ERP** Use o campo **Numero ordem** — corresponde ao `orderExternalId` enviado na criação do pedido.

**4. Confira os valores** Some as linhas de _Valor de face_ e _Taxa de desconto_ da mesma NF/parcela. O resultado é o valor líquido recebido por aquela duplicata.

> 📘 **Leitura dos valores**
>
> Valores **positivos** em _Valor BRL_ representam pagamentos feitos pela CrediPay à sua empresa. Valores **negativos** representam cobranças (taxas de desconto, reembolsos etc.).

***

## Campos da tabela

Cada linha representa uma transação dentro de um desembolso — um par de **NF + duplicata + tipo de lançamento**.

| Campo                           | Descrição                                                                                                                                                      |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Chave NF**                    | Chave de acesso de 44 dígitos da NF-e, conforme emitida no SEFAZ. Identificador único de cada Nota Fiscal.                                                     |
| **Parcela**                     | Número da duplicata dentro da NF. Ex.: parcela `1` de `2` = primeiro boleto de uma NF com dois vencimentos.                                                    |
| **Pago por**                    | Entidade responsável pela transferência. Pode ser a _Credix Finance Securitizadora III S.A._ ou o _CrediPay FIDC_.                                             |
| **Referencia**                  | Identificador único da TED/PIX. Aparece na descrição da transferência no extrato bancário.                                                                     |
| **Criado em**                   | Data de registro da transação na CrediPay. Para _Valor de face_ e _Taxa de desconto_, coincide com a data do desembolso.                                       |
| **Numero NF**                   | Número sequencial da NF (extraído da Chave NF). Útil para consulta rápida sem digitar os 44 dígitos.                                                           |
| **Tipo Transacao**              | Natureza do lançamento. Veja [Tipos de transação](#tipos-de-transação).                                                                                        |
| **Valor BRL**                   | Valor em reais. Positivo = pago pela CrediPay. Negativo = cobrado pela CrediPay. A soma de todos os valores de um mesmo _Referencia_ = valor total da TED/PIX. |
| **Desembolsado em**             | Data em que a transferência foi efetivamente realizada.                                                                                                        |
| **Vencimento**                  | Data de vencimento da duplicata, conforme acordado entre vendedor e comprador.                                                                                 |
| **Total parcelas na NF**        | Quantidade total de duplicatas geradas para esta NF. Ex.: `2` = NF parcelada em 2 boletos.                                                                     |
| **Numero ordem**                | Identificador externo do pedido no ERP do vendedor (`orderExternalId`). Use para cruzar com seus pedidos internos.                                             |
| **Banco Pagador**               | Código ISPB/COMPE do banco remetente da transferência.                                                                                                         |
| **Agência Pagador**             | Agência bancária do remetente.                                                                                                                                 |
| **Banco Destino**               | Código ISPB/COMPE do banco destinatário (sua conta).                                                                                                           |
| **Agência Destino**             | Agência bancária de destino.                                                                                                                                   |
| **Dígito Agência Destino**      | Dígito verificador da agência de destino (quando aplicável).                                                                                                   |
| **Conta Destino**               | Número da conta bancária de destino.                                                                                                                           |
| **Dígito Conta Destino**        | Dígito verificador da conta de destino.                                                                                                                        |
| **Valor Total Desembolso (R$)** | Valor total da TED/PIX à qual esta transação pertence. Todas as linhas de um mesmo _Referencia_ têm o mesmo valor aqui.                                        |

***

## Tipos de transação

| Tipo                             | Sinal | Descrição                                                                                                                                                                           |
| -------------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Valor de face**                | ➕     | Valor bruto do recebível antecipado — montante total da duplicata conforme emitida na NF.                                                                                           |
| **Taxa de desconto**             | ➖     | Desconto cobrado pela CrediPay pelo serviço de antecipação, proporcional ao prazo entre desembolso e vencimento. _Valor de face_ + _Taxa de desconto_ = valor líquido da duplicata. |
| **Taxa de transacao**            | ➖     | Eventuais taxas adicionais cobradas pela operação.                                                                                                                                  |
| **Reembolso**                    | ➖     | Devolução ao comprador por cancelamento ou ajuste de pedido. Descontado do próximo desembolso do vendedor.                                                                          |
| **Ajuste reembolso**             | ±     | Correção sobre um reembolso anterior, considerando o tempo decorrido entre o pagamento e a devolução.                                                                               |
| **Coobrigacao**                  | ➖     | Acionamento da cláusula de coobrigação em caso de inadimplência do comprador.                                                                                                       |
| **Repagamento apos Coobrigacao** | ➕     | Devolução ao vendedor após recuperação do valor em uma operação de coobrigação.                                                                                                     |
| **Repagamento**                  | ➕     | Devolução ao vendedor por pagamento realizado diretamente pelo comprador fora da plataforma.                                                                                        |

***

## Como a CrediPay realiza as transferências

Os pagamentos podem ser originados por duas entidades, o que impacta como aparecem no extrato:

### Credix Finance Securitizadora III S.A.

Todas as transações do dia são agrupadas em **uma única TED/PIX diária**. Você verá um único crédito no extrato consolidando múltiplas NFs e duplicatas.

### CrediPay Fundo de Investimento em Direitos Creditórios (FIDC)

Cada recebível é liquidado individualmente, gerando **uma TED/PIX separada por duplicata**. Você verá múltiplos créditos no extrato, cada um correspondendo a uma NF específica.

> 📘 **Dica**
>
> Em ambos os casos, use o campo **Referencia** para localizar a transferência no extrato e o campo **Chave NF** para identificar as notas incluídas.

***

## Indicadores do período

| Indicador               | Descrição                                                                                     |
| ----------------------- | --------------------------------------------------------------------------------------------- |
| **Total Desembolsado**  | Soma de todas as TED/PIX realizadas no período. Valor bruto antes de descontos e ajustes.     |
| **Nº de Desembolsos**   | Quantidade de transferências bancárias distintas. Cada desembolso pode agrupar múltiplas NFs. |
| **Ticket Médio**        | Valor médio por transferência (Total Desembolsado ÷ Nº de Desembolsos).                       |
| **Face Value Total**    | Soma dos valores de face de todos os recebíveis antecipados no período.                       |
| **Descontos Aplicados** | Soma das taxas de desconto cobradas. Valor negativo deduzido do Face Value.                   |
| **Reembolsos**          | Total devolvido à CrediPay por reembolsos de compradores no período.                          |
| **NFs Únicas**          | Quantidade de Notas Fiscais distintas nos desembolsos do período.                             |
| **Pedidos Únicos**      | Quantidade de pedidos únicos (`orderExternalId`) liquidados no período.                       |
