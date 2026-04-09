---
title: Funcionalidades da plataforma
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: Entenda os status dos pedidos
  pages:
    - type: basic
      slug: status-guide
      title: Guia de status
---
Na plataforma da CrediPay, existem diferentes formas de iniciar um pedido, mas o processo como um todo segue a mesma lógica. A maioria das etapas são semelhantes, mudando apenas alguns momentos específicos de acordo com a forma escolhida.

O fluxo abaixo mostra, de forma clara, como o processo acontece do início ao fim, desde a criação do pedido até a finalização com os boletos gerados para pagamento.

<Image align="center" src="https://files.readme.io/1f1c9aa12d6cd5677e7eaa229603a1387835ab48b4e53a846c20fcdf82fea6f5-seller_platform.png" />

# Acesso ao Dashboard CrediPay

Assim que a sua conta for aprovada na CrediPay, você já pode acessar o painel da plataforma para começar a gerenciar seus pedidos.

* URL de acesso: [https://app.credipay.credix.finance/](https://app.credipay.credix.finance/)
* Login com as credenciais da sua conta previamente cadastrada.

<Image align="center" width="600px" src="https://files.readme.io/19c874df321d8353ecfc26318115133a0e07d2d444b20bebb109c0ed5d4d0913-Frame_1.png" />

<br />

# 2. Como adicionar um novo pedido

Na seção "Pedidos", você pode iniciar uma nova operação clicando em **"Adicionar Pedido(s)"**, no topo da tela.

Depois, escolha como quer criar o pedido:

* **Enviar NF-e**(XML): Cria a ordem automaticamente com as informações do XML
* **Digitar Manualmente**: formulário para preencher as informações da ordem sem a necessidade da Nota Fiscal. A ordem só será finalizada se a Nota Fiscal for enviada e aprovada.

<Image align="center" width="600px" src="https://files.readme.io/2f113ba375195ad90e78b4e9a85692b1516cef4d47df9c0c410a7d0abff82c0a-Frame_2.png" />

<br />

### Criar pedido com envio de NF-e

Se você já tiver o arquivo XML da Nota Fiscal, pode enviar direto e o sistema cria o pedido automaticamente.

* Faça o upload do XML da NF-e.
* O sistema cria o pedido com base nas informações da nota.
* O comprador é notificado por e-mail.
* Assim que o comprador aprova, o pedido já é aceito.

<Image align="center" width="600px" src="https://files.readme.io/4f163454b2ac35b36f3975e48b2cc4cf515d8e56d99998c0af2b347b909c302f-image.png" />

<br />

### Criar pedido manualmente

Se preferir, você pode criar o pedido preenchendo os dados manualmente.

Antes de tudo, você vai precisar informar o **CNPJ do comprador.** O sistema vai verificar se ele existe na base e se possui limite de crédito disponível.

Se estiver tudo certo, aí sim você pode seguir preenchendo os demais dados do pedido:

* Valor estimado da ordem
* Código interno do pedido (referência)
* Prazo de pagamento

Depois de preencher todas essa informações:

* Clique em **“Checar detalhes do comprador”**
* Valide as informações e clique em **“Criar Pedido”**

O comprador vai receber um e-mail com o pedido para revisão e aprovação.

<Image align="center" width="400px" src="https://files.readme.io/9542af629abedd8cf8c6fb3bf9cfe144c59bcf0d302f831b54a7d1eb1e4e327a-image.png" />

<br />

# Aprovação do comprador

Após criar o pedido, o comprador precisará aprová-lo antes de seguir com o processo.

* Ele acessa o link enviado por e-mail.
* Revisa os dados da operação.
* Faz a aprovação.

Se o pedido foi criado com XML, a aprovação conclui automaticamente o processo.

<Image align="center" width="400px" src="https://files.readme.io/399ccc35e2290798be6c29ab6dd31fe543dbe0d5eed1451d352208c129817a7a-image.png" />

<br />

# Envio e validação da nota fiscal

Se o pedido foi criado manualmente, você deve enviar a nota fiscal (XML) depois da aprovação do comprador. O sistema valida automaticamente as informações.

Regras para a nota fiscal ser aceita, válidas para ambos os métodos de envio (na ordem e pós criação da ordem):

1. O valor da nota deve estar dentro do limite de crédito disponível do comprador.
2. A data de vencimento precisa respeitar o prazo definido no pedido.
3. Os CNPJs (seu e do comprador) devem bater com os informados no pedido.
4. A nota não pode ter sido usada antes na plataforma.
5. O endereço de entrega deve ser compatível com o endereço fiscal do CNPJ.
6. A nota precisa estar aprovada na SEFAZ (produção).

Imagem: Tela com status de validação da nota (Não tenho).

<br />

# Geração automática dos boletos

Após a validação da nota, os boletos serão gerados automaticamente e enviados para o e-mail do comprador.

Para visualizar os boletos na plataforma, é só atualizar a tela do pedido e ver em detalhes.

<br />

# Visualização e reembolsos

Você pode acompanhar os detalhes da operação e, se necessário, solicitar reembolso (total ou parcial).

Acesse o menu de três pontos ao lado do pedido:

* Clique em **“Ver detalhes do pedido”** para ver todos os boletos emitidos:

<Image align="center" width="600px" src="https://files.readme.io/d50638c57ff70e5b8ff63366e6abd23b33f31ad6a140f06d0690f29d62068861-Frame_4.png" />

<br />

* Solicitar reembolso parcial ou total do pedido:

<Image align="center" width="300px" src="https://files.readme.io/fd4defd63c4b3993f46345b19d49d6071e77a037a5cab3bb6e543fcf37904489-image.png" />

<br />

Se tiver qualquer dúvida sobre o uso da plataforma, o time da CrediPay está à disposição para ajudar.\
Entre em contato pelo nosso canal de suporte ou com o responsável da sua operação.
