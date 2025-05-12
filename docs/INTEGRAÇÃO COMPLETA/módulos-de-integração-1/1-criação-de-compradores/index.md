---
title: 1. Criação de compradores
excerpt: >-
  Embora o endpoint ofereça praticidade, recomendamos sempre iniciar pela
  importação em massa via lista, garantindo limites mais altos logo no primeiro
  uso.
deprecated: false
hidden: true
metadata:
  robots: index
---
A API de Análise de Crédito oferece avaliação de crédito em tempo real e onboarding automatizado de novos compradores na plataforma da Credix. Substituindo processos manuais por um fluxo de análise totalmente automatizado, ela proporciona aos vendedores visibilidade quase imediata sobre a elegibilidade dos compradores e seus limites de crédito. Com essa integração via API, a Credix permite que seus parceiros acelerem o fluxo de negociações, reduzam a carga operacional e escalem a concessão de crédito com fluidez e baixo atrito.

<br />

| Status   | Description                                                                                                                                                                |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Created  | A solicitação de análise foi recebida, mas ainda não foi iniciada. Normalmente, esse é um estado transitório logo após o envio da solicitação.                             |
| Pending  | O processo de análise ou onboarding está em andamento. Esse status abrange tanto etapas síncronas quanto assíncronas da execução.                                          |
| Finished | A solicitação de análise foi concluída com sucesso. A análise de crédito quanto o onboarding foram bem-sucedidos.                                                          |
| Failed   | O fluxo de análise ou onboarding encontrou um erro. Consulte o campo `errorReason` para obter mais detalhes. Esse caso pode exigir investigação ou reprocessamento manual. |