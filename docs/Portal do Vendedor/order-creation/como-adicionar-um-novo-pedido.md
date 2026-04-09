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

  <Image align="center" border={true} src="https://files.readme.io/2b1888a60896a00fe86f0b636046d4b9e95ed54fab9a8206f89ac506af71b2b6-Screenshot_2026-04-09_at_09.25.49.png" className="border" />

  <br />

## Criar pedido com envio de NF-e

Se você já tiver o arquivo XML da Nota Fiscal, pode enviar direto e o sistema cria o pedido automaticamente.

* Faça o upload do XML da NF-e.
* O sistema cria o pedido com base nas informações da nota.
* O comprador é notificado por e-mail.
* Assim que o comprador aprova, o pedido já é aceito.      

  <Image align="center" border={true} src="https://files.readme.io/b639fc6bdd3f4f5da711180b05ec919047e441a3fe1a166d8d8749ebbd929be4-Screenshot_2026-04-09_at_09.27.49.png" className="border" />

  <br />

## Criar pedido manualmente

Se preferir, você pode criar o pedido preenchendo os dados manualmente.

<Image align="center" border={true} src="https://files.readme.io/a4b326a9d1fe6c7635169690d58877247d0ba631a33d6502293270d9af6b74e9-Screenshot_2026-04-09_at_09.48.55.png" className="border" />

Antes de tudo, você vai precisar informar o **CNPJ do comprador.** O sistema vai verificar se ele existe na base e se possui limite de crédito disponível.

Se estiver tudo certo, aí sim você pode seguir preenchendo os demais dados do pedido:

### Comprador  

Nesta etapa, você identifica o cliente para o qual a venda está sendo feita.

* CNPJ do Comprador: Insira o CNPJ da empresa cliente.
* Botão "Buscar": Após digitar o CNPJ, clique em buscar. O sistema validará automaticamente se a empresa possui cadastro ativo e limite de crédito disponível na CrediPay para seguir com a operação.

### Detalhes do Vendedor

* Vendedor: Este campo geralmente é preenchido automaticamente pelo sistema com os dados da sua empresa (Razão Social e CNPJ), confirmando quem está emitindo o pedido.

### Informações de Contato

Dados da pessoa responsável por revisar e aprovar o pedido do lado do comprador. Se não houver contatos salvos, você precisará adicionar um novo.

* Nome: Primeiro nome do contato no cliente.
* Sobrenome: Sobrenome do contato.
* Email: E-mail corporativo (para onde será enviado o link de aprovação do pedido).
* Telefone: Número de contato (celular ou fixo).
* Botão "Adicionar contato": Salva as informações inseridas para vincular ao pedido.

### Enviar contato do financeiro

Área destinada a informar quem receberá as comunicações financeiras (como os boletos gerados).

* Checkbox "Mesmo contato do comprador": Se a pessoa que aprova o pedido for a mesma que realiza os pagamentos, basta marcar esta caixa para espelhar os dados preenchidos acima. Caso seja um departamento diferente, deixe desmarcado e preencha:
* Nome: Nome do responsável financeiro.
* E-mail: E-mail do departamento financeiro.
* Telefone: Telefone do setor.

### Endereço de Entrega

Local onde os produtos serão entregues ou o serviço prestado. Atenção: O endereço informado aqui deve ser compatível com o endereço que constará na Nota Fiscal (NF-e) gerada posteriormente.

* Endereço: Nome da rua/avenida e número.
* Complemento: Informações adicionais (galpão, sala, andar, bloco).
* CEP: Código Postal do local de entrega.
* Cidade: Município da entrega.
* Estado: UF da entrega.

### Resumo do Pedido

Informações financeiras e de controle interno da sua venda.

* Valor Total (R$): O valor bruto da negociação. Este valor deve ser o mesmo que constará na(s) Nota(s) Fiscal(is) e precisa estar dentro do limite de crédito do comprador.
* ID Externo: Um código de referência interno da sua empresa (como o número do pedido no seu ERP ou sistema de vendas), facilitando a conciliação futura.

### Processamento de Datas e Pagamento

Definição de como e quando a cobrança será gerada.

* Tipo de processamento de datas: Define a regra de vencimento. (Ex: DDE - Dias Depois da Entrega ou DDF - Dias Depois do Faturamento, que calcula o vencimento a partir da data de emissão da NF-e ou do aceite).
* Tipo de Parcelamento: Como o valor será dividido. (Ex: Pagamento único para cobrança à vista no vencimento, ou parcelado, caso disponível).
* Prazo de pagamento: A quantidade de dias concedidos para o pagamento (ex: 30 dias, 30/60/90 dias). Este prazo será refletido na data de vencimento dos boletos gerados após a validação da Nota Fiscal.

### Depois de preencher todas essa informações:

* Clique em **“Revisar Pedido”**
* Valide as informações e clique em **“Criar Pedido”**

O comprador vai receber um e-mail com o pedido para revisão e aprovação.

<br />
