---
title: Implementando CrediPay em minutos com IA
deprecated: false
hidden: true
icon: far fa-sparkles
metadata:
  robots: index
---
# Introdução

# IA na documentação

## Ask AI

![](https://files.readme.io/788aa15c6c3df26b2d6a524445f7dd8562ed246114e3497882877c424a0fbaa6-image.png)

<br />

Em todas as páginas da nossa documentação agora é possível usar a funcionalidade de 'Ask AI'. Através dela, você consegue abrir uma conversa com os principais LLMs do mercado, por onde você pode tirar dúvidas e pedir trechos de códigos. Ademais, é possível também acessar o markdown da página, o que é especialmente útil para ser inserido em IDE's como Cursor e Windsurf.

## llms.txt

Para inserir a documentação como um todo em seu ambiente de desenvolvimento, você deve acessar [https://docs.credipay.credix.finance/llms.txt](https://docs.credipay.credix.finance/llms.txt) , copiar e colar o texto. Vale ressaltar que também é possível (e recomendado) que sejam coladas **apenas** o conteúdo das páginas que se apliquem à parte que você esteja desenvolvendo no momento, visando deixar o contexto do seu modelo mais assertivo.

<br />

# Caso prático

Nesta seção, compartilharemos alguns prompts úteis para realizar uma implementação básica das APIs da CrediPay em um ERP. O objetivo é integrar os módulos de compradores, pedidos e faturamento do ERP às APIs do CrediPay sem usar código.

Neste projeto, usaremos o Cursor, porém as técnicas utilizadas aqui podem ser facilmente replicadas em outras ferramentas.

## Passo 0: Configurar variáveis de ambiente

Ante de começar, é necessário configurar as variáveis de ambiente. Para o desenvolvimento em questão, precisaremos de:

* CREDIPAY\_API\_KEY -> A chave de API da CrediPay
* CREDIPAY\_API\_URL -> A URL base do ambiente

Para mais informações, leia [Autenticação e ambientes](https://docs.credipay.credix.finance/update/docs/api-usage-authentication#/)

## Passo 1: Compradores

Como ponto de partida, temos uma página de compradores, onde o usuário pode selecionar um CNPJ e visualizar algumas informações básicas

![](https://files.readme.io/f73142ee1172f6c5ff22e8d9e1fdb914833889632c19bed8d53ef65a8f22b563-image.png)

O que queremos aqui é puxar o limite de crédito da CrediPay e disponibilizá-lo para o usuário no frontend. Para isso, enviaremos os prompts abaixo:

<Accordion title="Prompt 1.1: Criando o serviço" icon="fa-info-circle">
  Vamos começar a construir uma integração com a API da CrediPay. O primeiro passo que devemos construir é uma chamada do nosso server para a API GET v2/buyers da CrediPay (@[https://docs.credipay.credix.finance/reference/buyerscontroller\_getbuyers.md](https://docs.credipay.credix.finance/reference/buyerscontroller_getbuyers.md) ). Certifique-se de autenticar corretamente (@[https://docs.credipay.credix.finance/docs/api-usage-authentication.md](https://docs.credipay.credix.finance/docs/api-usage-authentication.md) ). A Chave de API (CREDIPAY\_API\_KEY) e o URL base (CREDIPAY\_API\_URL)  já estao configuradas como variáveis de ambiente.
</Accordion>

<Accordion title="Prompt 1.2: Ajustando o frontend" icon="fa-info-circle">
  Usando o que construimos, exponha o limite de crédito disponível na CrediPay para o CNPJ escolhido em @page.tsx
</Accordion>

Com estes dois prompts, nossa IA já foi capaz de realizar os ajustes necessários e trazer os dados da CrediPay para o frontend do nosso ERP!

![](https://files.readme.io/d9fab4f01680057c4df2f77731c7ab9dac9121f8d5c5d7ee238be5131c1c2046-image.png)