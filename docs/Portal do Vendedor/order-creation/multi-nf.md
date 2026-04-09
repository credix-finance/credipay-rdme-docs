---
title: Múltiplas Notas Fiscais por Pedido
deprecated: false
hidden: true
metadata:
  robots: index
---
## **Fluxo 1: Adicionando Múltiplas Notas Fiscais**

Este processo deve ser utilizado quando você possui várias notas para um mesmo pedido e deseja enviá-las em etapas.

1. Acesse o Pedido: Na lista de pedidos, localize e clique sobre o pedido desejado (ele deve estar com o status Aguardando NF-e).

<Image align="center" border={true} src="https://files.readme.io/904a0d87fd6ebd6152f87e5b346a86f4202f51574210a0d5a32eb1f11caf79e9-Screenshot_2026-04-08_at_19.10.07.png" className="border" />

<br />

2. Habilite o Recebimento Múltiplo: Role a página até a seção de Nota Fiscal. Antes de anexar o arquivo, marque a caixa de seleção "Vou enviar mais notas fiscais para este pedido".
3. Anexe a Nota Fiscal: Arraste e solte o arquivo XML da primeira NF-e na área indicada ou clique para selecionar o arquivo no seu computador.
4. Envie a Nota: Clique no botão Enviar Nota Fiscal.

<Image align="center" border={true} src="https://files.readme.io/9f3ffe849c4573c8b908717415641f3a868864daadffec2e80e45cd0aeece6fe-image.png" className="border" />

5. Confirme o Status: Uma mensagem de sucesso aparecerá e o status do pedido mudará para NF-es recebidas parcialmente (ou Processando NF-e). A nota adicionada aparecerá na lista de Notas Fiscais do pedido.

<Image align="center" border={true} src="https://files.readme.io/6d83d41406de858911c48dfe29f4a650c3292bce2fbd417db10f2ea79061fc94-Screenshot_2026-04-08_at_19.13.02.png" className="border" />

6. Repita o Processo: Como a caixa de seleção foi marcada, o pedido continua aberto para receber novas notas. Repita os passos de 2 a 4 para cada nota adicional que desejar inserir.

<br />

## **Fluxo 2: Enviando a Última Nota Fiscal**

Siga este passo quando for enviar a última nota fiscal pertencente ao pedido, encerrando o ciclo de recebimento.

1. Acesse a Seção de Envio: No mesmo pedido (agora com status NF-es recebidas parcialmente), vá até a seção de upload.
2. Desabilite o Recebimento Múltiplo: Certifique-se de que a caixa "Vou enviar mais notas fiscais para este pedido" esteja desmarcada. Isso sinaliza ao sistema que esta é a última nota.
3. Anexe e Envie: Faça o upload do último arquivo XML e clique em Enviar Nota Fiscal.

<Image align="center" border={true} src="https://files.readme.io/9fb2546dbe359cebdd9ce8096555f9815c14e9ddd96835889532e89065116358-Screenshot_2026-04-08_at_19.13.39.png" className="border" />

4. Validação: O sistema processará a nota final e o status do pedido será atualizado para capturado/processado, avançando para a próxima etapa e bloqueando a adição de novas notas.

<br />

## **Fluxo Alternativo: Finalização Manual de Captura**

Se o pedido já recebeu uma ou mais notas (status NF-es recebidas parcialmente), mas você percebeu que não há mais notas para enviar e deseja encerrar o pedido sem fazer um novo upload, siga os passos abaixo:

1. Acesse o Pedido Parcial: Abra o pedido que encontra-se com o status NF-es recebidas parcialmente.
2. Acione a Finalização: Localize e clique no botão Finalizar captura na parte inferior da tela.

<Image align="center" border={true} src="https://files.readme.io/04e4403df0d9ae7ee72e282fa5c5f34b498f39a895bf36caf6a0ce8273b9c92b-image.png" className="border" />

<br />

3. Confirme a Ação: Um modal de confirmação aparecerá alertando que nenhuma nova nota poderá ser enviada. Clique em Confirmar.    

<Image align="center" border={true} src="https://files.readme.io/02fcd7d348a4ee1ba8d2f947aca388f4d126e6ea8189838a84640f304ec5f34f-Screenshot_2026-04-08_at_19.15.01.png" className="border" />

4. Conclusão: O status do pedido será atualizado no sistema, encerrando o ciclo de notas fiscais para aquele pedido específico.
