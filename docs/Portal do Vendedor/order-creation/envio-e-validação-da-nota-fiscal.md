---
title: Envio e validação da nota fiscal
deprecated: false
hidden: false
metadata:
  robots: index
---
Se o pedido foi criado manualmente, você deve enviar a nota fiscal (XML) depois da aprovação do comprador. O sistema valida automaticamente as informações.

Regras para a nota fiscal ser aceita, válidas para ambos os métodos de envio (na ordem e pós criação da ordem):

1. O valor da nota deve estar dentro do limite de crédito disponível do comprador.
2. A data de vencimento precisa respeitar o prazo definido no pedido.
3. Os CNPJs (seu e do comprador) devem bater com os informados no pedido.
4. A nota não pode ter sido usada antes na plataforma.
5. O endereço de entrega deve ser compatível com o endereço fiscal do CNPJ.
6. A nota precisa estar aprovada na SEFAZ (produção).

Imagem: Tela com status de validação da nota (Não tenho).
