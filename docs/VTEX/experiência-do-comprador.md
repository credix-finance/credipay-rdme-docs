---
title: Experiência do comprador
excerpt: >-
  A jornada de compra a crédito dentro da VTEX: análise em tempo real, escolha
  de parcelas e o que muda com a análise antecipada.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Análise de crédito em tempo real

***

A análise acontece em dois momentos possíveis:

* **No login** — se o comprador ainda não foi analisado. Requer [VTEX IO](/project/credix-credipay/v2.1/docs/vtex-io-análise-antecipada).
* **No checkout** — quando ele escolhe transacionar com crédito.

No checkout, três cenários são possíveis: limite suficiente para a transação, limite parcial ou ausência de limite. A integração da CrediPay identifica automaticamente os dois últimos e realiza uma análise de crédito em tempo real usando apenas o CNPJ, atribuindo um novo limite em minutos — sem formulário e sem documento.

## Com e sem análise antecipada

***

A análise em tempo real leva de 1 a 2 minutos. **Onde** essa espera acontece muda bastante a conversão.

**Sem VTEX IO** — login → navega → checkout → consulta de limite → _espera de 1 a 2 min_ → confirma → pedido. O comprador já montou o carrinho e já escolheu a forma de pagamento quando é interrompido. É o ponto de maior abandono.

**Com VTEX IO** — a análise dispara no login e roda em segundo plano enquanto o comprador navega. Quando ele chega ao checkout, o limite já está pronto e não há espera.

Recomendado para lojas de alto volume. Veja [VTEX IO — análise antecipada](/project/credix-credipay/v2.1/docs/vtex-io-análise-antecipada).

## Reavaliação de crédito

***

Se a análise recusar ou aprovar apenas parcialmente, o comprador tem uma segunda chance. Ele pode pedir reavaliação fornecendo:

* **Open Finance** — conecta a conta bancária para compartilhar extratos e uso de cartão.
* **Documentos** — envia DRE, Balanço Patrimonial e notas fiscais de venda.

Os agentes de IA da CrediPay processam esses dados e, se aprovado, o comprador é notificado de que já pode transacionar.

## Criação do pedido e pagamento

***

Com limite disponível, o comprador escolhe o número de parcelas, visualiza as datas de vencimento e confirma a compra no modal da CrediPay, sem sair da VTEX. O valor da transação é debitado do limite disponível e o pedido segue para o vendedor faturar e enviar.

O intervalo padrão é de 30 dias entre parcelas:

* **1x** — vencimento em 30 dias.
* **2x** — vencimentos em 30 e 60 dias.
* **3x** — vencimentos em 30, 60 e 90 dias.

Para cada parcela, a CrediPay gera um boleto com opção de pagamento via PIX.

<Callout icon="📘" theme="info">
  ### A cobrança é toda da CrediPay

  O vendedor não gera boleto e não cobra o comprador. Se o seu ERP emite boleto automaticamente, ele precisa ser configurado para não fazer isso em pedidos CrediPay — caso contrário o comprador recebe duas cobranças.
</Callout>

## Acompanhamento do limite

***

Sob demanda, a CrediPay pode exibir o limite total e o limite utilizado do comprador dentro do próprio ambiente VTEX. Veja [Recursos adicionais](/project/credix-credipay/v2.1/docs/recursos-adicionais).

<br />
