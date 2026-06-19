---
title: Fluxo da operação
excerpt: >-
  Depois de configurada, a integração roda automaticamente. Veja quem faz o quê
  em cada etapa, da compra ao recebimento.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Faturamento e desembolso

<HTMLBlock>{`
<div style="position: relative; padding-bottom: 64.74820143884892%; height: 0;"><iframe src="https://www.loom.com/embed/e872a0d9bf154a2b80edd54969b8acb9?sid=6a18171d-9be0-45fa-892b-bc297606c676" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>
`}</HTMLBlock>

Com o meio de pagamento instalado na VTEX, a CrediPay monitora quando os pedidos recebem uma NF. Assim que a VTEX recebe o XML da NF, ele é transmitido automaticamente à CrediPay.

Tendo recebido a NF, a CrediPay provisiona o montante a ser pago, que será desembolsado na conta do vendedor.

## As etapas, de ponta a ponta

1. **Pedido confirmado** — o comprador confirma no checkout. O pedido é criado na VTEX e na CrediPay; o limite do comprador é reservado.
2. **Mercadoria despachada e NF-e emitida** — você fatura normalmente. O ERP gera a NF-e com as duplicatas nas datas calculadas e envia à VTEX.
3. **NF-e capturada automaticamente** — a VTEX repassa o XML. A CrediPay valida a NF-e e registra o recebível (duplicata) na CERC.
4. **Desembolso** — com a NF-e validada, o valor é provisionado e cai na sua conta.
5. **Cobrança ao comprador** — os boletos/PIX são gerados nas datas de vencimento. A CrediPay cobra e assume o risco.

> 📘 O gatilho do processo é a NF-e
>
> Enquanto um pedido não recebe a nota fiscal, ele fica reservando limite do comprador sem que você tenha sido pago. Emitir a NF-e rápido acelera o seu recebimento — acompanhe os pendentes no relatório de pedidos.

<br />