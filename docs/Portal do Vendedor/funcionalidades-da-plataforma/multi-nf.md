---
title: Múltiplas Notas Fiscais por Pedido
deprecated: false
hidden: false
metadata:
  robots: index
---
## **Fluxo 1: Adicionando Múltiplas Notas Fiscais**

Este processo deve ser utilizado quando você possui várias notas para um mesmo pedido e deseja enviá-las em etapas.

1. Acesse o Pedido: Na lista de pedidos, localize e clique sobre o pedido desejado (ele deve estar com o status Aguardando NF-e).

![](https://files.readme.io/536e23ff14560c389976de12d2adf58f38a987bb0ea28b17a915d20a2cb50434-Screenshot_2026-04-08_at_19.10.07.png)

2. Habilite o Recebimento Múltiplo: Role a página até a seção de Nota Fiscal. Antes de anexar o arquivo, marque a caixa de seleção "Vou enviar mais notas fiscais para este pedido".
3. Anexe a Nota Fiscal: Arraste e solte o arquivo XML da primeira NF-e na área indicada ou clique para selecionar o arquivo no seu computador.
4. Envie a Nota: Clique no botão Enviar Nota Fiscal.

![](https://files.readme.io/ddb4579f51e7f26e7f6938a49af2a4333d47361e38253553593c2abc33be2202-Screenshot_2026-04-08_at_19.12.23.png)

5. Confirme o Status: Uma mensagem de sucesso aparecerá e o status do pedido mudará para NF-es recebidas parcialmente (ou Processando NF-e). A nota adicionada aparecerá na lista de Notas Fiscais do pedido.

<Image align="center" border={true} src="https://files.readme.io/06980716d5c14463bbcaaf03bf073fda9b49c309784cf95f0c3513295c2c5700-Screenshot_2026-04-08_at_19.13.02.png" className="border" />

6. Repita o Processo: Como a caixa de seleção foi marcada, o pedido continua aberto para receber novas notas. Repita os passos de 2 a 4 para cada nota adicional que desejar inserir.

<br />

## **Fluxo 2: Enviando a Última Nota Fiscal**

Siga este passo quando for enviar a última nota fiscal pertencente ao pedido, encerrando o ciclo de recebimento.

1. Acesse a Seção de Envio: No mesmo pedido (agora com status NF-es recebidas parcialmente), vá até a seção de upload.
2. Desabilite o Recebimento Múltiplo: Certifique-se de que a caixa "Vou enviar mais notas fiscais para este pedido" esteja desmarcada. Isso sinaliza ao sistema que esta é a última nota.
3. Anexe e Envie: Faça o upload do último arquivo XML e clique em Enviar Nota Fiscal.

![](https://files.readme.io/03db61b7265b6728d7a41c461f12a138cb65c8d0f425b182e24ca02ae2f289c3-Screenshot_2026-04-08_at_19.13.39.png)

4. Validação: O sistema processará a nota final e o status do pedido será atualizado para capturado/processado, avançando para a próxima etapa e bloqueando a adição de novas notas.

<br />

## **Fluxo Alternativo: Finalização Manual de Captura**

Se o pedido já recebeu uma ou mais notas (status NF-es recebidas parcialmente), mas você percebeu que não há mais notas para enviar e deseja encerrar o pedido sem fazer um novo upload, siga os passos abaixo:

1. Acesse o Pedido Parcial: Abra o pedido que encontra-se com o status NF-es recebidas parcialmente.
2. Acione a Finalização: Localize e clique no botão Finalizar captura na parte inferior da tela.  

![](https://files.readme.io/2894118bace6359013e8e06c28b77fae6f03fe243e0f6708b0a215d9516f9b11-Screenshot_2026-04-08_at_19.14.29.png)

3. Confirme a Ação: Um modal de confirmação aparecerá alertando que nenhuma nova nota poderá ser enviada. Clique em Confirmar.

<Image align="center" border={true} src="https://files.readme.io/02fcd7d348a4ee1ba8d2f947aca388f4d126e6ea8189838a84640f304ec5f34f-Screenshot_2026-04-08_at_19.15.01.png" className="border" />

4. Conclusão: O status do pedido será atualizado no sistema, encerrando o ciclo de notas fiscais para aquele pedido específico.