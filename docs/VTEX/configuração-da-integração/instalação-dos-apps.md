---
title: Instalação dos Apps
deprecated: false
hidden: false
metadata:
  robots: index
---
Esta etapa é executada pelo seu time, quem tem acesso ao VTEX CLI e ao repositório da loja. O time de Integrações CrediPay fornece o que for necessário e acompanha, mas a execução acontece do seu lado.

Pré-requisito: VTEX CLI instalado e autenticado na conta da loja.

## 1. Apps da CrediPay

***

A partir da pasta VTEX do repositório da sua loja:

```bash
vtex install credixpartnerbr.credipay
vtex install credixpartnerbr.credipay-connector
```

* `credixpartnerbr.credipay` — renderiza a tela de confirmação do pagamento dentro do checkout: resumo do pedido, parcelas e confirmação da compra.
* `credixpartnerbr.credipay-connector` — conecta a loja ao Payment Provider Protocol da VTEX. É quem cria, cancela, liquida e reembolsa pagamentos.

## 2. Checkout UI Custom

***

A CrediPay depende do app de interface personalizada de checkout da VTEX. Se ele ainda não estiver instalado:

```bash
vtex install vtex.checkout-ui-custom@0.20.1
```

<Callout icon="📘" theme="info">
  ### Confirme a versão antes de instalar

  A versão fixada acima é a homologada no momento desta documentação. Alinhe com o time da CrediPay para confirmar qual é a versão vigente.
</Callout>

## 3. Interface personalizada de checkout

***

Por padrão, a VTEX exibe o parcelamento como _"Pagamento à vista"_ ou _"3x de R$ X"_, sem as datas de vencimento. Como na CrediPay o comprador está escolhendo prazos de pagamento e não parcelas de cartão, a data importa mais que o número.

O ajuste é feito no app **Interface personalizada de checkout** (_Checkout UI Custom_), na aba **JS**, e reescreve os rótulos das opções para incluir o vencimento de cada parcela. Partindo do intervalo padrão de 30 dias, ele transforma:

* `Pagamento à vista — R$ 500,00` em `1x de R$ 500,00 — vence 30/07`
* `3x de R$ 166,67` em `3x de R$ 166,67 — 30/07, 29/08, 28/09`

**O código é fornecido pelo time da CrediPay.** Cole na aba JS e **ative** a personalização.

<Callout icon="🚧" theme="warn">
  ### Não altere o script por conta própria

  Ele depende de seletores do DOM do checkout VTEX. Se a sua loja usa um tema de checkout customizado, o script pode precisar de ajuste — nesse caso, acione o time da CrediPay em vez de editar.
</Callout>

## 4. Verificar o que foi instalado

***

```bash
vtex list
```

Confirme que `credixpartnerbr.credipay` está na versão mais recente. Se estiver desatualizado:

```bash
vtex update
```

Próximo passo: [VTEX IO — análise antecipada](/project/credix-credipay/v2.1/docs/vtex-io-análise-antecipada), opcional mas recomendado para lojas de alto volume.

<br />
