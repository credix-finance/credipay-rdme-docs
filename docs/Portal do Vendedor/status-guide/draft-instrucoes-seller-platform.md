---
title: (draft) instrucoes seller platform
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
**Se eu integrar apenas este módulo, como já consigo transacionar com a CrediPay?**

Juntamente da API, oferecemos também uma [Plataforma Web](https://app.credipay.credix.finance/orders/) (solicite o acesso ao seu gerente de contas) por onde integradores pode realizar todas as ações. 

## Enviar Notas Fiscais

Pedidos criados via API aparecerão na tela desta plataforma, e uma vez confirmados pelo comprador, exibirão o status NF-e necessária. Assim, basta selecionar a opção enviar NF-e, e realizar o upload do XML da Nota Fiscal do pedido em questão

<Image align="center" src="https://files.readme.io/41a918663d4e2573b095f78dc01402c1d3a6d23d72e2a0eb8678b8c031a5acc4-image.png" />

## Emitir reembolsos e cancelamentos

Caso ocorra algum problema na entrega do pedido que faça com que o valor da cobrança seja menor do que o da NF enviada (ex. produtos danificados, recusados, extravio, etc.), isso deverá ser comunicado para que os boletos sejam ajustados. Para isso, temos a opção ‘Emitir reembolso’, por onde o valor reembolsado será passado para nós. Com o reembolso emitido, os boletos serão automaticamente ajustados para considerar o valor atualizado da cobrança.

> 💡 **ATENÇÃO**
>
> Uma vez feito, um reembolso não pode ser revertido.

![](https://files.readme.io/0ef775fa1afd7a0f297031546454b6441fd21fbf32d8c5ed7faba8b9e9040bb9-image.png)

## Buscar boletos

Assim que os boletos estiverem disponíveis, eles poderão ser visualizados na parte de detalhes do pedido. Basta selecionar a opção ‘Ver detalhes do pedido’ e acessar a página de cada arquivo.

![](https://files.readme.io/f71ba3cdf2f6881197c6a672d27c2e5fcdb032d712f259693a302ea3effd16a6-image.png)
