---
title: Integração Parcial
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: order-creation
      title: Funcionalidades da plataforma
    - type: basic
      slug: módulos-de-integração-1
      title: Etapas de integração
---
# Introdução

A integração com a CrediPay foi projetada para ser implementada de forma gradual, permitindo que você aproveite os benefícios que oferecemos à medida que avança em cada etapa da integração. Esta abordagem progressiva possibilita começar com uma integração mínima e ir automatizando cada processo no seu próprio ritmo, realizando manualmente as etapas ainda não integradas via API através da plataforma web da CrediPay.

# Implementação por etapas

## Cenário 1: Integração da Etapa 1 (Criação de pedido)

**O que você integra via API:**

- Endpoint GET v2/buyers para consultar condições de pagamento
- Endpoint POST v2/orders para criar pedidos

**O que você faz manualmente na plataforma:**

- Formalização do pedido (confirmação e envio de NF)
- Acesso aos boletos
- Reembolsos e cancelamentos

Neste cenário, após criar um pedido via API, você acessa a plataforma CrediPay para enviar manualmente a nota fiscal, acompanhar pagamentos e gerenciar eventuais reembolsos.

<br />

## Cenário 2: Integração das Etapas 1 e 2 (Criação e Formalização)

**O que você integra via API:**

- Tudo do cenário anterior
- Endpoint POST v2/order/{orderId}/capture para envio da nota fiscal

**O que você faz manualmente na plataforma:**

- Acesso aos boletos
- Reembolsos e cancelamentos

Com a integração da etapa 2, a criação e formalização do pedido ocorrem automaticamente via API, enquanto as demais ações podem ser realizadas através da plataforma web.

<br />

## Cenário 3: Integração das Etapas 1, 2 e 4 (Adicionando Cancelamentos/Reembolsos)

**O que você integra via API:**

- Tudo dos cenários anteriores
- Endpoint POST v2/order/{orderId}/cancel para cancelamentos
- Endpoint POST v2/order/{orderId}/refund para reembolsos

**O que você faz manualmente na plataforma:**

- Acesso aos boletos

Neste estágio avançado, você já automatizou a maioria dos processos, precisando acessar a plataforma apenas para monitoramento.

## Cenário 4: Integração Completa (Todas as etapas)

Todas as operações são realizadas via API, com a plataforma servindo apenas como interface alternativa para visualização e operações excepcionais.

<br />

# Vantagens da implementação progressiva

Esta abordagem por etapas oferece importantes benefícios durante o processo de integração:

- Início rápido: Comece a operar com CrediPay com esforço técnico mínimo, porém já oferecendo os benefícios de melhores condições de pagamento aos seus clientes
- Aprendizado gradual: Familiarize-se com o fluxo completo antes de automatizá-lo
- Validação por partes: Teste cada componente antes de avançar para o próximo
- Flexibilidade de desenvolvimento: Priorize recursos conforme necessidade do negócio

# Conclusão

A implementação progressiva da CrediPay permite que você comece a oferecer financiamento aos seus clientes rapidamente, com um esforço técnico inicial reduzido. À medida que sua integração avança, as operações manuais são gradualmente substituídas por processos automatizados via API, aumentando a eficiência e reduzindo o esforço operacional.  
Comece hoje mesmo implementando a primeira etapa e utilize nossa plataforma para as demais ações enquanto evolui na sua jornada de integração. Se precisar de suporte em qualquer fase do processo, nossa equipe está à disposição para auxiliá-lo.