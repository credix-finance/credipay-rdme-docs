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
