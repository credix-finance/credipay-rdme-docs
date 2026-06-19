---
title: Configuração da integração
excerpt: >-
  A integração tem dois lados: o que se ajusta na **VTEX** e o que se ajusta no
  seu **ERP**. O time de Integrações CrediPay acompanha cada etapa.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Na VTEX

***

- **Confirmar o CNPJ da conta** — o CNPJ da conta VTEX deve ser o mesmo onboardado na CrediPay. Envie o nome da conta (account name) ao time CrediPay.
- **Adicionar a CrediPay como provedor de pagamento** — em Configurações da loja → Pagamentos → Provedores, adicione a CrediPay com a App Key e o App Token fornecidos pelo time CrediPay.
- **Criar o meio de pagamento e a condição** — crie um pagamento customizado com o nome exato `Boleto a prazo` e a condição de pagamento vinculada ao provedor CrediPay.
- **Instalar o app de checkout** — o time CrediPay instala o app e o conector e aplica o ajuste que exibe as datas de vencimento no seletor de parcelas.

> 🚧 O nome importa
>
> O meio de pagamento precisa se chamar exatamente `CrediPay`, `Boleto a prazo CrediPay` ou `Boleto a prazo` (sensível a maiúsculas). Qualquer outro nome impede o pagamento.

# Integração com ERP

***

Com a integração ERP ↔ VTEX já existente, o fluxo de NF-e continua o mesmo. Há apenas dois ajustes a garantir.

## Criação do pedido

**Meio de pagamento**

Para o ERP aceitar o pedido vindo da VTEX, é necessário configurar um meio de pagamento específico para a CrediPay. Assegure-se de que esse meio de pagamento **não gere boletos** para o comprador, já que a cobrança será feita pela CrediPay.

## Faturamento

Se o pedido foi criado corretamente na etapa anterior, o faturamento é relativamente simples. Cada parcela deve entrar na Nota Fiscal como uma _duplicata_ — portanto, se temos 3 parcelas (installments = 3), devemos ter 3 duplicatas, vencendo em 30, 60 e 90 dias.

Em termos técnicos, o XML deve conter a tag `dup`, uma para cada parcela (a primeira terá número 1, a segunda 2, a terceira 3 — normalmente gerado de forma automática pelo ERP). O vencimento e o valor de cada duplicata na NF serão usados para a emissão dos boletos. Por exemplo: uma duplicata de R$1000 com vencimento em 25/10/2025 gera um boleto exatamente com esses parâmetros.

## Envio da NF à CrediPay

O envio da NF à CrediPay é **obrigatório** — é o que dispara o desembolso. O envio deve ocorrer somente após a aprovação da Secretaria da Fazenda. Em termos técnicos, o XML deve conter a tag `nfeProc` para ser aceito. Isso, junto com a presença das duplicatas, é o que garante que a NF está pronta para ser usada em uma operação de crédito.

Existem **3 formas** de fazer esse envio — escolha a que melhor se encaixa na sua operação:

* **Pela VTEX (automático)** — com o meio de pagamento instalado, a CrediPay monitora a VTEX e recebe o XML assim que a nota é faturada. Ao faturar na VTEX, um dos parâmetros é o `invoiceUrl`: é fundamental enviar um URL público apontando **diretamente** para o arquivo XML da NF, terminando em `.xml`.
* **Via API da CrediPay** — envie o XML diretamente para a CrediPay pela API, sem depender do faturamento na VTEX. Indicado para integrações que já controlam a emissão pelo ERP.
* **Manual, pela plataforma do vendedor** — faça o upload do XML pela plataforma da CrediPay. Útil para casos pontuais ou quando o envio automático não ocorreu.

> 📘 Requisitos da NF-e, em resumo
>
> * Tag `nfeProc` presente (NF-e aprovada pela SEFAZ).
> * Uma tag `dup` por parcela, com valor e vencimento batendo com o parcelamento.
> * No envio pela VTEX, `invoiceUrl` público, terminando em `.xml`.

# Estender via API

***

Para casos além do fluxo padrão, há um conjunto de APIs para consultar compradores, limites, pedidos e desembolsos. Veja as demais páginas desta documentação para a referência completa.