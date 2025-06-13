---
title: Implementando CrediPay em minutos com IA
deprecated: false
hidden: false
icon: far fa-sparkles
metadata:
  robots: index
---
# Introdução

***

A inteligência artificial está rapidamente se tornando uma parceira essencial no desenvolvimento de software, não apenas nos códigos que escrevemos, mas também na maneira como consumimos e mantemos a documentação técnica. Este guia foi criado para mostrar, passo a passo, como aproveitar os recursos de Ask AI e do arquivo llms.txt para turbinar o seu fluxo de trabalho com as APIs da CrediPay. Aqui você encontrará boas práticas, prompts prontos para uso e um caso prático completo que ilustra como integrar compradores, pedidos e faturamento em um ERP sem escrever uma linha de código. Use-o como ponto de partida, adapte-o às necessidades do seu projeto e descubra como a IA pode transformar tarefas repetitivas em processos rápidos, precisos e colaborativos.

# IA na documentação

***

## Ask AI

![](https://files.readme.io/788aa15c6c3df26b2d6a524445f7dd8562ed246114e3497882877c424a0fbaa6-image.png)

<br />

Em todas as páginas da nossa documentação agora é possível usar a funcionalidade de 'Ask AI'. Através dela, você consegue abrir uma conversa com os principais LLMs do mercado, através dos quais você pode tirar dúvidas e pedir trechos de códigos. Ademais, é possível também acessar o markdown da página, o que é especialmente útil para inserção em IDE's como Cursor e Windsurf.

## llms.txt

Para inserir a documentação como um todo em seu ambiente de desenvolvimento, você deve acessar [https://docs.credipay.credix.finance/llms.txt](https://docs.credipay.credix.finance/llms.txt) , copiar e colar o texto. Vale ressaltar que também é possível (e recomendado) que seja colado **apenas** o conteúdo das páginas que se apliquem à parte que você esteja desenvolvendo no momento, visando deixar o contexto do seu modelo mais assertivo.

<br />

# Caso prático

***

Nesta seção, compartilharemos alguns prompts úteis para realizar uma implementação básica das APIs da CrediPay em um ERP. O objetivo é integrar os módulos de compradores, pedidos e faturamento do ERP às APIs do CrediPay sem usar código.

Neste projeto, usaremos o Cursor, porém as técnicas utilizadas aqui podem ser facilmente replicadas em outras ferramentas. Vale ressaltar que os prompts utilizados neste processo não devem ser estritamente copiados em seu ambiente, mas podem servir como referência para os seus próprios prompts.

## Passo 0: Configurar variáveis de ambiente

Antes de começar, é necessário configurar as variáveis de ambiente. Para o desenvolvimento em questão, precisaremos de:

* CREDIPAY\_API\_KEY -> A chave de API da CrediPay
* CREDIPAY\_API\_URL -> A URL base do ambiente

Para mais informações, leia [Autenticação e ambientes](https://docs.credipay.credix.finance/update/docs/api-usage-authentication#/)

## Passo 1: Compradores

Como ponto de partida, temos uma página de compradores, onde o usuário pode selecionar um CNPJ e visualizar algumas informações básicas

![](https://files.readme.io/f73142ee1172f6c5ff22e8d9e1fdb914833889632c19bed8d53ef65a8f22b563-image.png)

O que queremos aqui é puxar o limite de crédito da CrediPay e disponibilizá-lo para o usuário no frontend. Para isso, enviaremos os prompts abaixo:

<Accordion title="Prompt 1.1: Criando o serviço" icon="fa-info-circle">
  Vamos começar a construir uma integração com a API da CrediPay. O primeiro passo que devemos construir é uma chamada do nosso server para a API GET v2/buyers da CrediPay ([https://docs.credipay.credix.finance/reference/buyerscontroller\_getbuyers.md](https://docs.credipay.credix.finance/reference/buyerscontroller_getbuyers.md) ). Certifique-se de autenticar corretamente ([https://docs.credipay.credix.finance/docs/api-usage-authentication.md](https://docs.credipay.credix.finance/docs/api-usage-authentication.md) ). A Chave de API (CREDIPAY\_API\_KEY) e o URL base (CREDIPAY\_API\_URL)  já estão configuradas como variáveis de ambiente.
</Accordion>

<Accordion title="Prompt 1.2: Ajustando o frontend" icon="fa-info-circle">
  Usando o que construimos, exponha o limite de crédito disponível na CrediPay para o CNPJ escolhido em @page.tsx
</Accordion>

Com estes dois prompts, nossa IA já foi capaz de realizar os ajustes necessários e trazer os dados da CrediPay para o frontend do nosso ERP!

![](https://files.readme.io/d9fab4f01680057c4df2f77731c7ab9dac9121f8d5c5d7ee238be5131c1c2046-image.png)

<br />

## Passo 2: Pedidos

Nosso ERP possui também uma tela para criação de pedidos. Nela, podemos escolher o comprador, inserir o endereço de entrega, forma de pagamento, etc. Nosso objetivo agora é permitir que o usuário crie um pedido utilizando o limite de crédito CrediPay.

![](https://files.readme.io/bc40f61fa26e38e038c402f3e3942e60a481fa21339ad56e8fb10b21ba6da2b8-image.png)

### Forma de pagamento

O primeiro passo é habilitar o sistema a oferecer a forma de pagamento CrediPay. Para isso, podemos enviar os seguintes prompt:

<Accordion title="Prompt 2.1: Nova forma de pagamento" icon="fa-info-circle">
  Atualize minha lista de formas de pagamento e inclua a forma CrediPay. Ela deve permitir que o usuário escolha opções de pagamento em 1, 2 ou 3 vezes. Reflita esta mudança também na página de criação de pedidos ( @page.tsx )
</Accordion>

Como resultado, agora podemos escolher a forma de pagamento CrediPay

![](https://files.readme.io/e82b15e6364bbfd83db4e64db8830652db35001938adbfe4800122abc1ba119d-image.png)

### Exibindo e checando o limite de crédito disponível

É importante que o limite de crédito disponível do comprador também seja exibido na tela de criação de pedidos, para que o usuário saiba o quanto pode inserir nesse pedido.

<Accordion title="Prompt 2.2: Limite de crédito na página de pedidos" icon="fa-info-circle">
  Na página de criação de pedidos  @NewOrderPage() use nosso serviço @credipay.ts  para exibir o limite de crédito disponível da CrediPay após o usuário selecionar um comprador. Se o comprador nao for encontrado na CrediPay, exiba 0
</Accordion>

Com isso, agora conseguimos checar o limite de crédito quando selecionamos um comprador.

![](https://files.readme.io/a962b9315524bbe48c352d3565c7aa54e6722a30a72bbb2ab5d2103508de1bf2-image.png)

Também é importante assegurar que a opção de pagar com CrediPay não possa ser seleciona caso não haja limite suficiente. Para isso, podemos rodar o prompt:

<Accordion title="Prompt 2.3: Bloqueando CrediPay caso não haja limite" icon="fa-info-circle">
  Ajuste o formulário de criação de pedido @OrderForm.tsx para que o usuário só possa selecionar a opção CrediPay caso o valor total do pedido seja menor ou igual ao limite de crédito disponível com a CrediPay
</Accordion>

E como resultado, a partir da agora não conseguiremos mais optar por transacionar com CrediPay caso não haja limite:

![](https://files.readme.io/9460a6a621d3e6cd8383a5e7f3ae7c22333492917ff3f02c203b0d91f1523292-image.png)

### Enviando o pedido para a CrediPay

Agora, precisamos nos assegurar que, assim que o usuário submeter o pedido, ele será enviado à CrediPay para que seja realizada a reserva de limite de crédito. Além disso, devemos nos assegurar de que o pedido não será criado internamente caso não seja aceito pela CrediPay - nesse caso, o usuário também deve ser informado da recusa.

Para isso, o primeiro passo é integrar o endpoint de criação de pedidos:

<Accordion title="Prompt 2.4: Implementando o endpoint de pedidos" icon="fa-info-circle">
  Na nossa integracao com a credipay @credipay.ts , implemente agora o endpoint de criacao de pedidos @[https://docs.credipay.credix.finance/reference/orderscontroller\_postorder.md](https://docs.credipay.credix.finance/reference/orderscontroller_postorder.md) . Certifique-se de autenticar corretamente @[https://docs.credipay.credix.finance/docs/api-usage-authentication.md](https://docs.credipay.credix.finance/docs/api-usage-authentication.md) .
</Accordion>

Em seguida aplicar ao nosso fluxo:

<Accordion title="Prompt 2.5: Integrando endpoint de pedidos no fluxo" icon="fa-info-circle">
  Usando o que acabamos de construir, ajuste a criação de pedidos @handleCreateOrder() para primeiro tentar criar o pedido na CrediPay. Se houver um erro, mostrar ao usuário na @NewOrderPage() . Se bem sucedido, criar um pedido na base de dados, já com o order id da CrediPay - nao devemos criar um pedido na base de dados caso nao seja criado na CrediPay
</Accordion>

<Accordion title="Prompt 2.6: Exibindo o id do pedido no frontend" icon="fa-info-circle">
  Exiba o order id da credipay na pagina do pedido @OrderDetailPage()
</Accordion>

E pronto! De agora em diante, o pedido será criado automaticamente na CrediPay, e veremos o id CrediPay em nosso frontend:

![](https://files.readme.io/f814530768b0ae8e5d656605e995ceaaa38bcb7e2c35802ff813d7a10a337dca-image.png)

<br />

## Passo 3: Faturamento

A última etapa a ser integrada é a de faturamento. Como nosso ERP demonstrativo não tem a capacidade de emitir uma NF real, nós vamos realizar uma simulação por meio de um upload de XML, e assim enviar o XML para a CrediPay.

Como de costume, vamos começar integrando o endpoint para captura do XML:

<Accordion title="Prompt 3.1: Implementando endpoint de captura de XML" icon="fa-info-circle">
  Na nossa integracao com a credipay @credipay.ts , implemente agora o endpoint de captura de xmls @[https://docs.credipay.credix.finance/reference/orderscontroller\_captureorder.md](https://docs.credipay.credix.finance/reference/orderscontroller_captureorder.md) . Certifique-se de autenticar corretamente (@[https://docs.credipay.credix.finance/docs/api-usage-authentication.md](https://docs.credipay.credix.finance/docs/api-usage-authentication.md)   )
  Tenha em mente que:

  * O id do pedido enviado no URL é o ID do pedido na CrediPay
  * Content Type deve ser multipart form data
</Accordion>

Em seguida aplicar ao nosso fluxo

<Accordion title="Prompt 3.2: Integrando endpoint de captura de XML ao nosso fluxo" icon="fa-info-circle">
  Usando o que acabamos de construir, ajuste a criação de notas fiscais @handleUpload()  para primeiro tentar criar o pedido na CrediPay. Certifique-se de passar o order id da CrediPay e nao o order id interno do sistema.
  Se houver um erro, mostrar ao usuário na @UploadInvoicePage()  . Se bem sucedido, atualizar o pedido na base de dados,  com os dados do arquivo - nao devemos atualizar o pedido na base de dados caso o xml nao seja aceito pela CrediPay.
</Accordion>

Com isso, o fluxo se torna completamente integrado, e toda vez que tivermos um novo XML de Nota Fiscal, ele será enviado à CrediPay. Quando um XML é enviado e aceito, a CrediPay considera a transação oficializada, e partir deste momento irá formalizar legalmente a operação, emitir os boletos para cobrança, e provisionar o montante para desembolso ao vendedor.

A partir daqui, não há mais nenhuma ação mandatória por parte do vendedor, ou seja, a integração está completa!

# Conclusão

***

A funcionalidade Ask AI e o arquivo llms.txt transformam a maneira como você consome a documentação da CrediPay: a primeira cria um canal direto com os principais modelos de linguagem para tirar dúvidas e gerar código sob demanda; o segundo leva todo o conteúdo (ou apenas as páginas relevantes) para dentro da sua IDE, oferecendo contexto instantâneo aos seus prompts. Com isso, o processo de leitura, compreensão e aplicação da documentação fica muito mais rápido e preciso, reduzindo retrabalho e acelerando o ciclo de desenvolvimento.

O caso prático mostrou como, guiado por prompts bem-estruturados, é possível integrar módulos de compradores, pedidos e faturamento em um ERP sem escrever código manual: desde configurar variáveis de ambiente e exibir limites de crédito, até criar pedidos condicionados ao limite e capturar XML de notas fiscais. Ao adotar esse fluxo orientado por IA, você automatiza tarefas repetitivas, garante consistência entre sistemas e libera tempo para focar em soluções criativas que agreguem valor ao produto.