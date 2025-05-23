---
title: Como funciona?
excerpt: >-
  Conheça as etapas que compõem o ciclo completo de um pedido com a CrediPay —
  da análise de crédito à conciliação dos pagamentos.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: >-
    🔀 Agora que você conhece o fluxo completo, veja como ele se adapta a
    diferentes canais de venda — como e-commerce e televendas.
  pages:
    - type: basic
      slug: canais-de-vendas
      title: Canais de vendas
---
### Ciclo de vida de um pedido

Antes de integrar, é importante entender a jornada completa de uma transação na CrediPay — da avaliação de crédito até a conciliação dos repasses. Esse fluxo serve como referência para todos os modelos de integração, e ajuda seu time técnico a identificar onde e como a solução se conecta com seus sistemas.

<Image align="center" width="500px" src="https://files.readme.io/4e14b618110bc6d49c13391c3e9187a5b72d19ed3ae16c805cd176ab5d87bed0-Order_life_cycle.svg" />

### Etapas do ciclo de vida de um pedido

| Etapa                           | O que acontece                                                                            | Como funciona na prática                                                 |
| ------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **1. Análise de crédito**       | Avaliação automática do comprador com base no CNPJ, score interno e limites de exposição. | Executada pela CrediPay previamente.                                     |
| **2. Criação do pedido**        | Envio das informações do pedido: valor, itens, prazos, dados do comprador.                | Pode ser feito via API (`POST /v2/orders`) ou diretamente no painel web. |
| **3. Confirmação da operação**  | A proposta de crédito é validada.                                                         | Confirmação automática (e-commerce) ou via link (televendas).            |
| **4. Envio da nota fiscal**     | Emissão e envio do XML da NF-e.                                                           | Realizado via API (`POST /v2/orders/{id}/capture`) ou painel web.        |
| **5. Validação do XML**         | Verificação automática de consistência fiscal.                                            | Pedido entra em pendência se houver erros no XML.                        |
| **6. Liquidação ao vendedor**   | Repasse dos valores líquidos.                                                             | Realizado após validação do XML. Prazo padrão: D+1.                      |
| **7. Cobrança ao comprador**    | Início do ciclo de pagamento.                                                             | A CrediPay assume a cobrança conforme o calendário de parcelas.          |
| **8. Reembolsos e conciliação** | Gestão de reembolsos, cancelamentos e acompanhamento financeiro.                          | Pode ser feito via API ou dashboard.                                     |