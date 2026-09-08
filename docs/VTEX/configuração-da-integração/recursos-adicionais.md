---
title: Recursos Adicionais
excerpt: 'Configurações complementares. '
deprecated: false
hidden: false
metadata:
  robots: index
---
A primeira é padrão em toda integração; as outras duas são ativadas sob demanda.

## Chave de API para dados transacionais

***

A CrediPay usa essa chave para ler os dados transacionais da loja, necessários para conciliação, relatórios e suporte.

* No canto superior direito do Admin VTEX, clique no seu perfil
* Vá em **Configurações da conta**
* Clique em **Criar chaves de API** → **Gerar chave**
* Em _Identificação da chave_, dê um nome, por exemplo `CrediPay - dados transacionais`
* Selecione o perfil **OMS Full access**
* Clique em **Gerar**

Compartilhe a chave gerada com o time da CrediPay pelo canal seguro combinado.

<Callout icon="🚧" theme="warn">
  ### O token aparece uma única vez

  A VTEX exibe o token apenas no momento da criação. Guarde antes de fechar a tela — se perder, é preciso gerar uma chave nova.
</Callout>

## Motor de impostos e juros por parcela

***

Disponível sob demanda, para lojas que precisam de regras fiscais ou de juros que variam por item e por meio de pagamento.

Quando o comprador inicia o checkout, a VTEX envia os dados do carrinho (`orderForm`) para um endpoint da CrediPay. Esse serviço aplica, item a item, as regras de imposto e de juros por parcela conforme o meio de pagamento escolhido — por exemplo, juros específicos para prazos CrediPay mantendo boletos comuns sem juros. Os valores calculados voltam e aparecem no carrinho na hora, com latência média abaixo de 0,40s por requisição.

A especificação da VTEX está em [Tax Services](https://developers.vtex.com/docs/guides/tax-services-specification). Fale com o time da CrediPay para avaliar se faz sentido no seu caso.

## Página de limite disponível

***

Disponível sob demanda. Exibe, dentro do ambiente VTEX, o limite total e o limite já utilizado do comprador — para que ele acompanhe o crédito disponível sem sair da loja.

<br />
