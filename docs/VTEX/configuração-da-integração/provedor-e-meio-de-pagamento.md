---
title: Provedor e Meio de Pagamento
deprecated: false
hidden: false
metadata:
  robots: index
---
Três objetos precisam existir na VTEX para a CrediPay aparecer no checkout: o **provedor**, o **meio de pagamento** e a **condição de pagamento**. Cada um gera um ID que será usado na etapa final.

<Callout icon="📘" theme="info">
  ### Anote os IDs conforme avançar

  Os três IDs desta página são pré-requisito para habilitar as parcelas. Sem eles, a última etapa não pode ser executada e o checkout fica limitado a pagamento à vista.
</Callout>

## 1. Provedor de pagamento

***

O time da CrediPay envia uma **App Key** e um **App Token** exclusivos da sua loja.

* No Admin VTEX, vá em **Configurações da loja → Pagamentos → Provedores**
* Clique em **Novo provedor**
* Busque por **CrediPay**
* Preencha a App Key e o App Token recebidos
* Salve

**Anote o&#x20;**`affiliationId` — depois de salvar, abra a página do provedor. O ID está na URL.

## 2. Meio de pagamento customizado

***

* Vá em **Configurações da loja → Configurações de pagamento → Pagamentos customizados → Promissória**
* Crie um novo pagamento
* Nome: `Boleto a prazo` — este é o texto que o comprador vê no checkout

**Anote o&#x20;**`paymentSystemId` — está na URL, e é um número entre **201 e 205**.

<Callout icon="🚧" theme="warn">
  ### O nome importa

  O meio de pagamento precisa se chamar exatamente `CrediPay`, `Boleto a prazo`, `Boleto a Prazo` ou `Boleto a prazo CrediPay` (sensível a maiúsculas). Qualquer outro nome, inclusive com espaço extra no fim, faz a criação do pagamento falhar e o comprador não consegue concluir a compra.
</Callout>

## 3. Condição de pagamento

***

* Ainda em **Configurações de pagamento**, vá em **Condições de pagamento**
* Crie uma nova usando o pagamento customizado recém-criado
* Selecione **provedor = CrediPay**
* Nome: `Boleto a prazo`
* Salve

**Anote o&#x20;**`ruleId` — está na URL.

<Callout icon="📘" theme="info">
  ### Até 10 minutos para refletir

  Esta etapa costuma demorar para propagar na VTEX. Se a condição não aparecer no checkout imediatamente, aguarde antes de recriar.
</Callout>

## 4. Habilitar as parcelas

***

Por padrão, a condição criada aceita apenas pagamento à vista. Para liberar o parcelamento é preciso uma chamada à API de instalações da VTEX. **Esta etapa é executada pelo time da CrediPay** — você só precisa fornecer os dados abaixo.

* `accountName` — o mesmo enviado no início da [configuração](/project/credix-credipay/v2.1/docs/configuração-da-integração)
* `affiliationId` — da URL do provedor de pagamento, item 1 desta página
* `paymentSystemId` — da URL do pagamento customizado, item 2. Número entre 201 e 205
* `ruleId` — da URL da condição de pagamento, item 3
* **Autenticação** — uma chave de API de Admin, ou o cookie `VtexIdclientAutCookie`

### Como obter o cookie de autenticação

Se optar pelo cookie em vez de uma chave de Admin:

* Logado no Admin VTEX, abra as **Ferramentas de desenvolvedor** (F12, ou botão direito → Inspecionar)
* Vá na aba **Application** → **Storage → Cookies**
* Copie o valor de `VtexIdclientAutCookie`

<Callout icon="🚧" theme="warn">
  ### Esse cookie é uma credencial de administrador

  Compartilhe apenas pelo canal seguro combinado com o time da CrediPay, nunca por e-mail ou chat aberto. Sempre que possível, prefira gerar uma chave de API de Admin dedicada — ela pode ser revogada depois, o cookie não.
</Callout>

## Como validar

***

Abra a loja, adicione um item ao carrinho e vá ao checkout com um CNPJ já aprovado. O meio **Boleto a prazo** deve aparecer, com as opções de parcelamento e as datas de vencimento visíveis.

Se não aparecer, veja [Solução de problemas](/project/credix-credipay/v2.1/docs/solução-de-problemas).

<br />
