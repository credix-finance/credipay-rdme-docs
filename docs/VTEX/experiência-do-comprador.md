---
title: Experiência do comprador
excerpt: >-
  Toda a experiência acontece dentro da VTEX. O comprador não sai da loja, não
  preenche cadastro longo e não envia documentos para comprar a prazo.
deprecated: false
hidden: true
metadata:
  robots: index
---
## Análise de crédito em tempo real

<HTMLBlock>{`
<div style="position: relative; padding-bottom: 58.82352941176471%; height: 0;">
  <iframe src="https://www.loom.com/embed/5add326975d24371bbf54d9a467eb8cc?sid=c1b336d8-fd9d-40e1-a326-14860ad50ca6" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
</div>
`}</HTMLBlock>

A CrediPay pode rodar uma análise de crédito em tempo real em 2 momentos da jornada do cliente:

- Quando o cliente loga, caso ainda não tenha sido analisado, ele será analisado.
- Quando um comprador chega ao checkout e deseja transacionar utilizando crédito. Aqui, 3 cenários podem ocorrer:
  - O comprador possui limite suficiente para completar a transação.
  - O comprador possui limite, mas não o suficiente para completar a transação.
  - O comprador não possui limite.

Dentro do checkout, a integração da CrediPay automaticamente identifica compradores nos cenários 2 e 3 e realiza uma análise de crédito em tempo real usando apenas o CNPJ. Assim, conseguimos atribuir um novo limite em minutos (dependendo da análise) e permitir que o cliente finalize a compra.

**Medidas de segurança nesta etapa**

- Analisamos centenas de dados do CNPJ para avaliar não só o risco de crédito, mas também de fraude. Alguns exemplos: se o CNPJ foi criado ou adquirido recentemente, se possui processos, entre outros.
- Analisamos também o histórico dos sócios, para garantir que não estejam envolvidos em outras atividades potencialmente fraudulentas.
- Além do nosso próprio modelo, o CNPJ é analisado por parceiros que possuem suas próprias regras de prevenção à fraude, com bases interbancárias, blacklists, entre outros.

> 📘 Acelere a aprovação no checkout
>
> A análise pode ser antecipada para o momento do **login** (recurso opcional). Assim, quando o comprador chega ao checkout, o limite já está pronto e não há espera — recomendado para lojas de alto volume.

<br />

## Reavaliação via Open Finance ou documentos

<HTMLBlock>{`
<div style="position: relative; padding-bottom: 64.75%; height: 0; width: 100%;">
  <iframe 
    src="https://www.linkedin.com/embed/feed/update/urn:li:ugcPost:7419808637797404672?compact=1" 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: none;" 
    allowfullscreen="" 
    title="Embedded post">
  </iframe>
</div>
`}</HTMLBlock>

Caso a análise inicial resulte em recusa ou aprovação parcial, ainda oferecemos uma oportunidade para o comprador obter o crédito necessário para fechar a compra. Nesse cenário, ele pode solicitar uma reavaliação da decisão, enviando dados adicionais:

- **Conexão Open Finance:** o comprador compartilha dados da conta bancária, como extrato e uso de cartão de crédito.
- **Documentos:** o comprador envia DRE, Balanço/Balancete e NFs de venda.

Esses dados são analisados por agentes de IA. Se aprovado, o comprador recebe uma comunicação de que agora está habilitado a transacionar.

<br />

## Criação de pedidos

Tendo limite de crédito, o comprador abre a tela de confirmação do pedido, vê um resumo da compra e, com um clique, finaliza sem sair do ambiente VTEX. Ao confirmar, o pedido é enviado à CrediPay e o valor é subtraído do limite disponível do cliente.

<Columns layout="auto">
  <Column>
    <Image align="center" src="https://files.readme.io/cf6cebfc0ac9c8fb5a71181b03676e90b51ee6a8a4a443611ca18d3b1f489c1a-image.png" />
  </Column>

  <Column>
    <Image align="center" src="https://files.readme.io/904ab304a0c414c7e7304121438606c9801ab6d17901d498ccd2c0071f42e603-image2.png" />
  </Column>
</Columns>

No checkout, o comprador começa escolhendo o número de parcelas. Em seguida, abre o modal, que exibe as datas de vencimento dos boletos do pedido.

**Nota:** como a VTEX permite configurar o número de parcelas, mas não as datas, assumimos 30 dias entre cada parcela. Um pedido de 3 parcelas, por exemplo, será 30-60-90.

| Parcelas escolhidas | Vencimentos dos boletos |
| ------------------- | ----------------------- |
| 1×                  | 30 dias                 |
| 2×                  | 30 e 60 dias            |
| 3×                  | 30, 60 e 90 dias        |

**Medidas de segurança nesta etapa**

- O servidor da CrediPay recebe dados diretamente do servidor da VTEX, impossibilitando ataques via manipulação do cliente.
- Serão aceitos pedidos com endereço de entrega apenas para o endereço do cartão CNPJ.

<br />

## Como o comprador paga

Para cada parcela, a CrediPay gera um boleto com opção de PIX. O comprador recebe o link do PDF, o código de barras e o QR Code, com o vencimento de cada parcela. **A cobrança é toda da CrediPay** — o vendedor não precisa gerar nem acompanhar boletos.
