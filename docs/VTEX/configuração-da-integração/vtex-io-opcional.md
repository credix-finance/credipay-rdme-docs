---
title: Vtex IO [Opcional]
deprecated: false
hidden: false
metadata:
  robots: index
---
Opcional, mas recomendado para lojas de alto volume. É a diferença entre o comprador esperar no checkout e não esperar.

## O problema que resolve

***

Quando um comprador não tem limite suficiente, a CrediPay dispara uma análise em tempo real. Sem VTEX IO, isso acontece **no checkout** — o comprador já escolheu os produtos, já escolheu a forma de pagamento, e é nesse momento que precisa aguardar de 1 a 2 minutos.

**Sem VTEX IO:** login → navega → checkout → consulta de limite → **espera de 1 a 2 min** → confirma → pedido.

O comprador é bloqueado no meio da compra. É o ponto de maior abandono de carrinho.

**Com VTEX IO:** login (_análise dispara em segundo plano_) → navega (_limite é atualizado_) → checkout → confirma → pedido.

A análise roda enquanto o comprador navega. Quando ele chega ao checkout, o limite já está atualizado e a compra segue sem espera.

## Por que vale a pena

***

* **Para o comprador** — zero espera no checkout, e o limite é conhecido antes de montar o carrinho.
* **Para o vendedor** — menos abandono de carrinho e menos cancelamento e reembolso pós-pedido, já que compradores de alto risco são identificados antes que o pedido exista.
* **Para a CrediPay** — menor exposição a fraude, menos carga de API no pico do checkout e aprovações mais precisas.

## Como instalar

***

Os apps são publicados sob o **seu** vendor VTEX, não o da CrediPay. Por isso a instalação exige publicá-los a partir do repositório da CrediPay.

### 1. Acesso ao repositório

A CrediPay concede acesso ao repositório Git.

```bash
git clone https://github.com/credix-finance/vtex-apps.git
```

### 2. Ajustar o vendor

Em **dois** arquivos de manifesto, troque o vendor `credixpartnerbr` pelo nome da sua conta VTEX:

* `handle-user-data-event/manifest.json`
* `send-user-data-event/manifest.json`

```json
"vendor": "suaconta",
```

### 3. Publicar

```bash
vtex publish
```

<Callout icon="📘" theme="info">
  ### A publicação leva cerca de 7 minutos

  É o tempo normal do processo da VTEX. Não interrompa.
</Callout>

### 4. Fazer deploy para master

```bash
vtex deploy
```

### 5. Instalar

```bash
vtex install suaconta.handle-user-data-event@0.0.2
vtex install suaconta.send-user-data-event@0.0.2
```

Substitua `suaconta` pelo vendor definido no passo 2 e confirme as versões com o time da CrediPay antes de instalar.

## O que cada app faz

***

* `send-user-data-event` — detecta o login do comprador na loja e envia o evento com o CNPJ para a CrediPay.
* `handle-user-data-event` — recebe o retorno e mantém o estado de limite atualizado durante a navegação.

## Como validar

***

Faça login na loja com um CNPJ sem limite ou com limite insuficiente. Navegue por alguns instantes e vá ao checkout. O limite deve estar disponível sem tela de espera.

Próximo passo: [Recursos adicionais](/project/credix-credipay/v2.1/docs/recursos-adicionais).

<br />
