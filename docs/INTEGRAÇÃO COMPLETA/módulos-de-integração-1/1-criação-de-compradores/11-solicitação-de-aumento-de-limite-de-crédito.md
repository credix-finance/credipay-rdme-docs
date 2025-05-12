---
title: 1.1 Solicitação de Aumento de Limite de Crédito
deprecated: false
hidden: true
metadata:
  robots: index
---
Esses endpoints permitem que vendedores ou plataformas solicitem um aumento no limite de crédito de um comprador e acompanhem o status da avaliação dessa solicitação. Eles facilitam o gerenciamento de limites de crédito de forma fluida, automatizando o envio e a análise dos pedidos, acelerando um processo que tradicionalmente era conduzido por equipes operacionais.

É importante destacar que a solicitação de limite está sujeita à análise e poderá ser recusada ou aprovada parcialmente.

| Status            | Description                                                              |
| ----------------- | ------------------------------------------------------------------------ |
| Created           | A solicitação foi recebida, mas ainda não foi processada                 |
| Pending           | A solicitação está atualmente em avaliação                               |
| Approved          | O valor total solicitado foi aprovado                                    |
| PartiallyApproved | Um limite inferior ao solicitado foi aprovado                            |
| Rejected          | A solicitação foi negada (consulte o campo reason para a explicação)     |
| Failed            | O processo de avaliação falhou devido a erros de sistema ou de validação |