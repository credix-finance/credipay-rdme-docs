---
title: Como adicionar um novo pedido
deprecated: false
hidden: true
metadata:
  robots: index
---
Na seção "Pedidos", você pode iniciar uma nova operação clicando em **"Adicionar Pedido(s)"**, no topo da tela.

Depois, escolha como quer criar o pedido:

* **Enviar NF-e**(XML): Cria a ordem automaticamente com as informações do XML
* **Digitar Manualmente**: formulário para preencher as informações da ordem sem a necessidade da Nota Fiscal. A ordem só será finalizada se a Nota Fiscal for enviada e aprovada.

<Image align="center" width="600px" src="https://files.readme.io/2f113ba375195ad90e78b4e9a85692b1516cef4d47df9c0c410a7d0abff82c0a-Frame_2.png" />

### Criar pedido com envio de NF-e

Se você já tiver o arquivo XML da Nota Fiscal, pode enviar direto e o sistema cria o pedido automaticamente.

* Faça o upload do XML da NF-e.
* O sistema cria o pedido com base nas informações da nota.
* O comprador é notificado por e-mail.
* Assim que o comprador aprova, o pedido já é aceito.

<Image align="center" width="600px" src="https://files.readme.io/4f163454b2ac35b36f3975e48b2cc4cf515d8e56d99998c0af2b347b909c302f-image.png" />

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
