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
A integração tem dois lados: o que se ajusta na **VTEX** e o que se ajusta no seu **ERP**. O time de Integrações CrediPay acompanha cada etapa.

Este guia existe para que o seu time saiba o que será pedido, em que ordem e por quê.

## Checklist da integração

***

Siga na ordem — cada etapa depende da anterior.

* **1. Pré-requisitos e dados da conta** — *vendedor, 5 min.* Confirmar o CNPJ e enviar o account name.
* **2. [Chave de aplicação e permissões](/project/credix-credipay/v2.1/docs/chave-de-aplicação-e-permissões)** — *vendedor, 15 min.* Criar o perfil de acesso e liberar a chave da CrediPay.
* **3. [Provedor e meio de pagamento](/project/credix-credipay/v2.1/docs/provedor-e-meio-de-pagamento)** — *vendedor, 25 min.* Cadastrar o provedor, criar o `Boleto a prazo` e a condição de pagamento.
* **4. [Instalação dos apps](/project/credix-credipay/v2.1/docs/instalação-dos-apps)** — *CrediPay, 25 min.* Instalar o app, o conector e o ajuste de checkout.
* **5. Habilitar as parcelas** — *CrediPay, 10 min.* Feito com os IDs coletados na etapa 3.
* **6. [Chave de API para dados transacionais](/project/credix-credipay/v2.1/docs/recursos-adicionais)** — *vendedor, 5 min.*
* **7. Integração ERP ↔ VTEX** — *vendedor.* Detalhada mais abaixo nesta página.
* **8. [VTEX IO — análise antecipada](/project/credix-credipay/v2.1/docs/vtex-io-análise-antecipada)** — *opcional, vendedor, 30 min.*

> 📘 Paciência com a propagação
>
> Várias configurações da VTEX levam até 10 minutos para refletir. Se algo não aparecer logo após salvar, aguarde antes de refazer — recriar o objeto costuma piorar o diagnóstico.

## Na VTEX

***

### Pré-requisitos e dados da conta

Antes de qualquer configuração técnica:

* **Valide o CNPJ** — o CNPJ da conta VTEX precisa ser um dos CNPJs onboardados na CrediPay. Se você vende por mais de um CNPJ, todos precisam estar cadastrados.
* **Envie o account name** — é o identificador da sua loja na VTEX, o `minhaloja` em `minhaloja.myvtex.com`.

Onde encontrar: no Admin VTEX, vá em **Marketplace → Sellers → Gerenciamento** e clique no seller. O CNPJ e o *id da conta* aparecem nessa tela.

O account name é usado em praticamente todas as etapas seguintes — envie ao time da CrediPay logo no início.

### Demais etapas

As etapas 2 a 6 estão detalhadas em páginas próprias, linkadas no checklist acima.

## Integração com ERP

***

Com a integração ERP ↔ VTEX já existente, o fluxo de NF-e continua o mesmo. Há apenas dois ajustes a garantir.

### Criação do pedido

**Meio de pagamento**

Para o ERP aceitar o pedido vindo da VTEX, é necessário configurar um meio de pagamento específico para a CrediPay. Assegure-se de que esse meio de pagamento **não gere boletos** para o comprador, já que a cobrança será feita pela CrediPay.

> 🚧 Cobrança duplicada
>
> Se o ERP emitir boleto além da CrediPay, o comprador recebe duas cobranças pelo mesmo pedido. É o erro de configuração mais comum na entrada do pedido.

### Faturamento

Se o pedido foi criado corretamente na etapa anterior, o faturamento é relativamente simples. Cada parcela deve entrar na Nota Fiscal como uma *duplicata* — portanto, se temos 3 parcelas (installments = 3), devemos ter 3 duplicatas, vencendo em 30, 60 e 90 dias.

Em termos técnicos, o XML deve conter a tag `dup`, uma para cada parcela (a primeira terá número 1, a segunda 2, a terceira 3 — normalmente gerado de forma automática pelo ERP). O vencimento e o valor de cada duplicata na NF serão usados para a emissão dos boletos. Por exemplo: uma duplicata de R$1000 com vencimento em 25/10/2025 gera um boleto exatamente com esses parâmetros.

Se o número de duplicatas não bater com o parcelamento do pedido, a nota é recusada na validação e o desembolso não acontece.

### Envio da NF à CrediPay

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

> 🚧 invoiceUrl atrás de login
>
> É a causa mais comum de nota não capturada. A CrediPay acessa a URL de fora da sua rede — teste abrindo o endereço em uma janela anônima. Se pedir autenticação, a captura automática não vai funcionar.

## Quando algo não funciona

***

A página [Solução de problemas](/project/credix-credipay/v2.1/docs/solução-de-problemas) lista os sintomas mais comuns, a causa provável de cada um e como corrigir.

<br />
