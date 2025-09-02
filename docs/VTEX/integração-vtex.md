---
title: Integração VTEX
deprecated: false
hidden: true
metadata:
  robots: index
---
# Introdução)

***

A CrediPay é uma solução completa para facilitar operações de crédito no ambiente B2B, integrada diretamente à plataforma VTEX. Este documento descreve as funcionalidades disponíveis, bem como aquelas que serão lançadas em breve, explicando como cada etapa da jornada, desde a análise de crédito até o faturamento, reembolsos e relatórios, foi pensada para tornar o processo de compra a prazo mais ágil, seguro e eficiente.

Nosso objetivo é permitir que vendedores ofereçam crédito de forma automatizada e com segurança, reduzindo riscos e aumentando a conversão de vendas. Para isso, integramos a análise de crédito em tempo real, garantimos a comunicação segura entre sistemas e disponibilizamos relatórios completos de acompanhamento e reconciliação.

# Funcionalidades

***

## Análise de crédito em tempo real

<HTMLBlock>{`
<div style="position: relative; padding-bottom: 58.82352941176471%; height: 0;">
  <iframe src="https://www.loom.com/embed/5add326975d24371bbf54d9a467eb8cc?sid=c1b336d8-fd9d-40e1-a326-14860ad50ca6" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" />
</div>
`}</HTMLBlock>

Quando um comprador chega ao checkout e deseja transacionar utilizando crédito, 3 cenários podem ocorrer:

1. O comprador possui limite suficiente para completar a transação
2. O comprador possui limite, mas não o suficiente para completar a transação
3. O comprador não possui limite

A integração da CrediPay automaticamente identifica compradores nos cenários 2 e 3, e realiza uma análise de crédito em tempo real usando apenas o CNPJ. Assim, conseguimos atribuir um novo limite em minutos (dependendo da análise de crédito) e permitir que este cliente finalize a compra.

Medidas de segurança nesta etapa

* Analisamos centenas de dados do CNPJ a fim de avaliar não só o risco de crédito, mas também de fraude. Alguns exemplos são se o CNPJ foi criado ou adquirido recentemente, se possui processos, entre outros.
* Analisamos também o histórico dos sócios, para garantir que não estejam envolvidos em outras atividades potencialmente fraudulentas.
* Além de nosso próprio modelo, o CNPJ é analisado também pelo BTG Pactual, que possui suas próprias regras de prevenção à fraude, envolvendo bases de dados interbancárias de fraude, blacklists, entre outros.

_Mais detalhes (conteúdo em inglês):_

[Fraud_Overview_June_2025.pdf](%5BEXT%5D%20CrediPay%20-%20Integra%C3%A7%C3%A3o%20VTEX%20231917cac58d80199df4e83907426f7e/Fraud_Overview_June_2025.pdf)

## Criação de pedidos

Tendo limite de crédito, o comprador conseguirá abrir a tela de confirmação de pedido, onde verá um resumo de sua compra, e com um clique consegue finalizar a compra sem sair do ambiente VTEX. Ao fazer isso, o pedido é enviado à CrediPay, e o valor da compra é subtraído limite de crédito disponível do cliente.

![image.png](%5BEXT%5D%20CrediPay%20-%20Integra%C3%A7%C3%A3o%20VTEX%20231917cac58d80199df4e83907426f7e/image.png)

![image.png](%5BEXT%5D%20CrediPay%20-%20Integra%C3%A7%C3%A3o%20VTEX%20231917cac58d80199df4e83907426f7e/image%201.png)

No nosso checkout, o comprador começa o processo escolhendo o número de parcelas com que deseja pagar. Depois, abre o modal, que exibirá as datas de vencimento dos boletos do pedido.

**Nota:** Como a VTEX permite configurar o número de parcelas mas não as datas, assumimos 30 dias entre cada parcela. Portanto, um pedido de 3 parcelas por exemplo será 30-60-90

Medidas de segurança nesta etapa

* O servidor da CrediPay recebe dados diretamente do servidor da VTEX, impossibilitando ataques via manipulação do cliente
* Serão aceitos pedidos com endereço de entrega apenas para o endereço do cartão CNPJ

## Faturamento

[https://www.loom.com/share/e872a0d9bf154a2b80edd54969b8acb9](https://www.loom.com/share/e872a0d9bf154a2b80edd54969b8acb9)

Com o meio de pagamento instalado no ambiente VTEX, a CrediPay consegue monitorar quando os pedidos criados recebem uma NF. Com isso, assim que a VTEX recebe um arquivo de XML de NF, ele automaticamente é transmitido à CrediPay.

Tendo recebido a NF, a CrediPay irá realizar o provisionamento do montante a ser pago, que será desembolsado em até 24h úteis na conta do vendedor. Para mais detalhes sobre reconciliação, veja [Relatórios](https://www.notion.so/Relat-rios-231917cac58d808d9d0ef099bdaf2f1b?pvs=21).

Como isso se integra ao ERP?

Com a integração ERP-VTEX configurada, não é necessário nenhum ajuste adicional, e as NFs fluirão automaticamente para a VTEX, e em seguida para a CrediPay. O ERP deve utilizar as datas de vencimento calculadas na criação do pedido como as datas de vencimento das duplicatas.

Medidas de segurança nesta etapa

* Checamos novamente o endereço de entrega, para garantir que é o mesmo do cartão CNPJ
* Ao receber uma NF, realizamos automaticamente os trâmites legais de aquisição do recebível (duplicata) junto à CERC, uma registradora de ativos de crédito, que por sua vez realizada validações diretamente com a Secretaria da Fazenda e com outras registradoras

## Reembolsos e Cancelamentos

Similarmente ao tópico anterior, a CrediPay receberá de forma automática os reembolsos e cancelamentos da VTEX, que por sua vez deve receber do ERP. Quando isto acontecer, os boletos serão ajustados automaticamente, para garantir uma cobrança coerente ao comprador. Além disso, o valor reembolsado será somado ao limite de crédito disponível do cliente, permitindo-o usar esse saldo para novas compras.

Buscando otimizar o processo, nós não requisitamos que o vendedor faça uma transferência para nos estornar os valores reembolsados, mas descontamos do adiantamento seguinte. Esse detalhamento pode ser encontrado na parte de [Relatórios](https://www.notion.so/Relat-rios-231917cac58d808d9d0ef099bdaf2f1b?pvs=21)

Como isso se integra ao ERP?

Com a integração ERP-VTEX configurada, não é necessário nenhum ajuste adicional, e os reembolsos e cancelamentos fluirão automaticamente para a VTEX, e em seguida para a CrediPay.

Medidas de segurança nesta etapa

* Nunca acataremos uma solicitação de reembolso ou cancelamento vinda diretamente do comprador. Nestes casos, o vendedor é quem nos deve informar o pedido e o valor a ser reembolsado.

## Relatórios

Em conjunto com a integração VTEX-CrediPay, entregamos também um dashboard por onde é possível acompanhar as principais métricas e dados da operação. Veja abaixo um descritivo de cada uma das seções:

*_certos dados foram ocultos para assegurar a privacidade de nossos usuários_

Reconciliação

Nesta aba, é possível visualizar, na maior granularidade possível, tudo o que está sendo pago e cobrado na relação entre CrediPay e vendedor.

![reconc.png](%5BEXT%5D%20CrediPay%20-%20Integra%C3%A7%C3%A3o%20VTEX%20231917cac58d80199df4e83907426f7e/reconc.png)

Limites de crédito

Nesta aba, é possível obter uma visão geral de todos os limites de crédito aprovados pela CrediPay, o quanto foram consumidos, e o quanto ainda está disponível

![download.png](%5BEXT%5D%20CrediPay%20-%20Integra%C3%A7%C3%A3o%20VTEX%20231917cac58d80199df4e83907426f7e/download.png)

Acompanhamento de pedidos e XML’s

Aqui, é possível acompanhar quais pedidos ainda não receberam um XML de Nota Fiscal, portanto estão ocupando limite de crédito do cliente sem que o vendedor tenha sido pago.

![download (1).png](%5BEXT%5D%20CrediPay%20-%20Integra%C3%A7%C3%A3o%20VTEX%20231917cac58d80199df4e83907426f7e/download_\(1\).png)

Cobrança

Na seção de cobrança, damos visibilidade dos casos em que ainda não conseguimos receber pelo pedido, e um detalhamento dos valores em aberto por comprador.

![download (2).png](%5BEXT%5D%20CrediPay%20-%20Integra%C3%A7%C3%A3o%20VTEX%20231917cac58d80199df4e83907426f7e/download_\(2\).png)

## Funcionalidades adicionais (API)

Caso seja necessário estender a integração com a CrediPay além dos tópicos mencionados acima, nós oferecemos também um conjunto de APIs, que pode ser encontrado aqui: [https://docs.credipay.credix.finance/](https://docs.credipay.credix.finance/reference/buyerscontroller_getbuyers#/)

# Integração com ERP

***

## Criação do pedido

**Meio de pagamento**

Para o ERP conseguir aceitar o pedido vindo da VTEX, é necessário que seja configurado um meio de pagamento específico para a CrediPay. Deve-se assegurar que este meio de pagamento não gere boletos para o comprador, já que a cobrança vai ser realizada pela CrediPay.

**Parcelas**

A VTEX enviará, no objeto do pedido, o número parcelas escolhido pelo comprador (por exemplo, no caso de 30-60-90, teremos `“installments”:3` ). O ERP deve possuir a lógica de ler esse dado e calcular as datas de vencimento das cobranças do pedido, que serão 30,60 e 90 dias após sua criação. Isso será importante na parte do faturamento. Portanto:

Installments = 1 → Pedido será pago em uma parcela, vencendo em 30 dias

Installments = 2 → Pedido será pago em duas parcelas de igual valor, vencendo em 30 e 60 dias

Installments = 3 → Pedido será pago em três parcelas de igual valor, vencendo em 30, 60 e 90 dias

## Faturamento

Se o pedido foi criando corretamente na etapa anterior, o faturamento deve ser relativamente simples. Cada parcela criada deve entrar na Nota Fiscal como uma _duplicata_ - portanto, se temos 3 parcelas por exemplo (installments = 3), devemos ter 3 duplicatas, vencendo em 30, 60 e 90 dias. Em termos técnicos, isso significa que o XML deve conter a tag `dup`, sendo uma para cada parcela do pedido. O vencimento e valor de cada duplicata na NF será usado para a emissão de boletos - por exemplo, se temos uma duplicata de R$1000 com vencimento em 25/10/2025, o boleto a ser gerado terá exatamente os mesmos parâmetros.

## Envio da NF à VTEX

O envio da NF à VTEX deve ocorrer somente após a aprovação da Secretaria da Fazenda para a NF. Em termos técnicos, isso quer dizer que o XML da NF deve conter a tag `nfeProc` para ser aceito. Isso, juntamente com a presença das duplicatas (etapa anterior), é o que garante que aquela NF está pronta para ser utilizada em uma operação de crédito.

Ao faturar um pedido na VTEX, um dos parâmetros a serem passados é o `invoiceUrl`. Neste campo, é fundamental que seja enviado um URL público **diretamente** para o arquivo XML da NF em questão. Esse é um URL que necessariamente acabará com ‘.xml’

Exemplo de URL: [https://www.webdanfe.com.br/danfe/exemplos/NFe_assinada.xml](https://www.webdanfe.com.br/danfe/exemplos/NFe_assinada.xml) (XML público)

# Conclusão

***

Com a CrediPay, compradores e vendedores contam com uma solução completa para transações B2B a prazo. Nossa proposta é simplificar o acesso ao crédito, automatizar processos e garantir uma experiência fluida em todas as etapas, da análise de crédito ao faturamento e acompanhamento financeiro.

Estamos comprometidos em evoluir continuamente nossa plataforma, oferecendo novas funcionalidades e mantendo um alto padrão de segurança e transparência. Conte com nosso time de integrações e suporte dedicado para garantir o sucesso da implementação e o máximo aproveitamento das soluções CrediPay em sua operação.
