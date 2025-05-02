---
title: 'Canais de vendas: e-commerce e televendas'
excerpt: >-
  Veja como a criação, confirmação e acompanhamento de pedidos varia conforme o
  canal de venda, e prepare sua integração de forma alinhada ao seu modelo de
  operação.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: >-
    Agora que você compreendeu as diferenças entre os canais de venda, o próximo
    passo é definir como integrar a CrediPay ao seu fluxo. Oferecemos três
    caminhos distintos de integração, que variam em nível de complexidade
    técnica e grau de automação.


    Cada modelo foi pensado para atender a diferentes perfis operacionais —
    desde quem precisa começar de forma rápida, até quem busca uma integração
    100% automatizada.
  pages:
    - type: basic
      slug: getting-started-integration-options
      title: Opções de Integração
---
### Definições e exemplos de aplicação

#### E-commerce

No e-commerce, o comprador finaliza a compra diretamente em um site ou aplicativo da empresa, de forma autônoma. A jornada é self-service: o comprador seleciona produtos, escolhe a condição de pagamento, confirma a operação e acompanha o andamento da compra diretamente pela plataforma.

_Exemplo de aplicação:_  
Uma plataforma de equipamentos industriais oferece parcelamento via boleto diretamente no checkout. O comprador escolhe a quantidade de parcelas, conclui o pedido e acessa seus boletos e limites futuros diretamente no portal.

#### Televendas

Em televendas (ou qualquer formato de vendas assistidas), um vendedor atua ativamente no processo. O pedido é criado em nome do comprador, por meio do ERP ou painel da empresa. A confirmação do pagamento exige uma etapa adicional: o comprador deve acessar e aprovar o link de pagamento enviado após a criação do pedido, garantindo que o comprador está ciente da venda sendo realizada em seu nome.

_Exemplo de aplicação:_  
Um distribuidor de autopeças realiza vendas por telefone. O vendedor cria o pedido manualmente, envia o link de pagamento ao comprador para confirmação, acompanha a emissão da nota fiscal e gerencia eventuais reembolsos ou informações de cobrança via painel da CrediPay.

### Diferenças operacionais

| Pontos de atenção                       | E-commerce                                                                                                                            | Televendas                                                                                                                      |
| :-------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------ |
| Confirmação do pedido                   | Confirmação automática no momento da finalização da compra pelo comprador                                                             | Envio de link de pagamento para o comprador, que deve confirmar manualmente antes da emissão da nota fiscal.                    |
| Identificação do vendedor               | Não aplicável.                                                                                                                        | Obrigatória. O vendedor é identificado pelo login (plataforma web) ou via campo dedicado na criação do pedido via API.          |
| Acesso às informações e funcionalidades | O comprador acessa diretamente boletos, limites de crédito, solicitações de reembolso e status dos pedidos pela plataforma integrada. | O vendedor gerencia todas as informações e presta suporte ao comprador via painel ou ERP, sem necessidade de acionar a CrediPay |

<br />

### Considerações técnicas

- No televendas, um pedido só é considerado válido após a confirmação do link de pagamento. Não será possível aceitar uma nota fiscal associada a um pedido não confirmado.
- A identificação do vendedor é obrigatória em todas as operações assistidas.
- No e-commerce, a integração pode disponibilizar todas as funcionalidades diretamente para o comprador, sem necessidade de intermediação humana.