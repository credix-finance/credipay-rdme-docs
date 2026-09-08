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
# Experiência do comprador

Toda a experiência acontece dentro da VTEX. O comprador não sai da loja, não
preenche cadastro longo e não envia documentos.

## Análise de crédito em tempo real

A análise acontece em dois momentos possíveis:

- **No login** — se o comprador ainda não foi analisado _(requer [VTEX IO](/docs/vtex-io-analise-antecipada))_
- **No checkout** — quando ele escolhe transacionar com crédito

No checkout, três cenários:

| Cenário           | O que acontece                                                    |
| ----------------- | ----------------------------------------------------------------- |
| Limite suficiente | Segue direto para a confirmação                                   |
| Limite parcial    | A CrediPay dispara uma análise em tempo real usando apenas o CNPJ |
| Sem limite        | A CrediPay dispara uma análise em tempo real usando apenas o CNPJ |

A integração identifica automaticamente os cenários 2 e 3 e atribui um novo
limite em minutos — sem formulário e sem documento.

## Com e sem análise antecipada

A análise em tempo real leva de 1 a 2 minutos. _Onde_ essa espera acontece muda
bastante a conversão.

### Sem VTEX IO — a espera cai no checkout

```
Login  →  Navega  →  Checkout  →  Consulta de limite  →  ⏳ 1–2 min  →  Confirma  →  Pedido
```

O comprador já montou o carrinho e já escolheu a forma de pagamento quando é
interrompido. É o ponto de maior abandono.

### Com VTEX IO — a espera desaparece

```
Login  →  Navega  →  Checkout  →  Confirma  →  Pedido
  ↓
 análise roda em
 segundo plano
```

A análise dispara no login e roda enquanto o comprador navega. Quando ele chega
ao checkout, o limite já está pronto.

Recomendado para lojas de alto volume. Veja
[VTEX IO — análise antecipada](/docs/vtex-io-analise-antecipada).

## Reavaliação de crédito

Se a análise recusar ou aprovar apenas parcialmente, o comprador tem uma segunda
chance. Ele pode pedir reavaliação fornecendo:

- **Open Finance** — conecta a conta bancária para compartilhar extratos e uso de
  cartão
- **Documentos** — envia DRE, Balanço Patrimonial e notas fiscais de venda

Os agentes de IA da CrediPay processam esses dados e, se aprovado, o comprador é
notificado de que já pode transacionar.

## Criação do pedido e pagamento

Com limite disponível, o comprador:

1. Escolhe o número de parcelas
2. Vê as datas de vencimento de cada parcela
3. Confirma a compra no modal da CrediPay, sem sair da VTEX

O valor da transação é debitado do limite disponível e o pedido segue para o
vendedor faturar e enviar.

### Parcelas e vencimentos

Exemplo: O intervalo padrão é de 30 dias entre parcelas:

| Parcelamento | Vencimentos      |
| ------------ | ---------------- |
| 1x           | 30 dias          |
| 2x           | 30 e 60 dias     |
| 3x           | 30, 60 e 90 dias |

Para cada parcela, a CrediPay gera um boleto com opção de pagamento via PIX.

### A cobrança é toda da CrediPay

O vendedor não gera boleto e não cobra o comprador. Se o seu ERP emite boleto automaticamente, ele precisa ser configurado para não fazer isso em pedidos CrediPay.

<br />

## Acompanhamento do limite

Sob demanda, a CrediPay pode exibir o limite total e o limite utilizado do
comprador dentro do próprio ambiente VTEX. Veja
[Recursos adicionais](/docs/recursos-adicionais#página-de-limite-disponível).
