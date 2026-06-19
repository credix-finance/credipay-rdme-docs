---
title: 'Visão geral '
deprecated: false
hidden: true
metadata:
  robots: index
---
# Visão geral

***

A CrediPay é uma solução completa para operações de crédito B2B, integrada diretamente à plataforma VTEX. A CrediPay aparece como meio de pagamento nativo dentro do checkout: o comprador compra a prazo com aprovação em minutos, e o vendedor recebe à vista, sem assumir o risco de inadimplência.

Esta documentação descreve a experiência do comprador, o que você precisa configurar, o fluxo da operação, os status de cada pedido e o acompanhamento financeiro.

<HTMLBlock>{`
<div style="border:1px solid #E6E3F1;border-radius:16px;padding:28px 30px;background:#F5F4FA;">
  <div style="font-size:22px;font-weight:700;color:#1A1730;line-height:1.3;">
    O comprador paga em <span style="color:#6D4AFF;">30 · 60 · 90 dias</span>.
    Você recebe em <span style="color:#12B886;">24h úteis</span>.
  </div>
  <div style="margin-top:8px;color:#6B6685;font-size:15px;">
    A CrediPay assume o crédito e a cobrança. Quem vende não espera o prazo do comprador para receber.
  </div>
</div>
`}</HTMLBlock>

## O que muda com a CrediPay

| Indicador                     | Sem CrediPay | Com CrediPay |
| ----------------------------- | ------------ | ------------ |
| Taxa de aprovação no checkout | \~50%        | \~79%        |
| Limite de crédito ofertado    | base         | +103%        |
| Ticket médio                  | R$ 24k       | R$ 34k       |
| Prazo de pagamento            | 28 dias      | até 90 dias  |

## Como funciona, em quatro etapas

1. **Análise de crédito** — no checkout (ou já no login), a CrediPay analisa o CNPJ do comprador e libera um limite em minutos, usando modelo próprio mais validação de parceiros.
2. **Pedido criado** — o comprador escolhe as parcelas e confirma. O pedido nasce ao mesmo tempo na VTEX e na CrediPay, e o limite é reservado.
3. **Nota fiscal** — seu ERP emite a NF-e normalmente. A VTEX repassa o XML para a CrediPay, que valida e registra o recebível.
4. **Desembolso e cobrança** — com a NF-e validada, o valor é desembolsado em até 24h úteis. A CrediPay cobra o comprador nos vencimentos.

> 📘 Comunicação segura
>
> Todos os dados da transação trafegam servidor-a-servidor entre VTEX e CrediPay — nunca pelo navegador do comprador. O endereço de entrega é validado contra o cadastro do CNPJ.

## O que você precisa ter

- Loja ativa na VTEX com o mesmo CNPJ que será onboardado na CrediPay.
- Integração ERP ↔ VTEX já funcionando para a emissão de NF-e.
- Capacidade de configurar um meio de pagamento que **não gere boletos próprios** — a cobrança é feita pela CrediPay.

<br />
