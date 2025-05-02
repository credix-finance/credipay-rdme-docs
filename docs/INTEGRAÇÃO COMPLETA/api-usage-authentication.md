---
title: Autenticação e ambientes
excerpt: Learn how to authenticate with the CrediPay API.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Chave de API - Staging

A API da CrediPay utiliza **chaves de API** para autenticar as requisições. Você pode solicitar sua chave de staging entrando em contato com nosso time pelo e-mail: [suporte-credipay@credix.finance](mailto:suporte-credipay@credix.finance) ou diretamente com o seu **gerente de contas**

> 💡 **Importante**
>
> Nunca compartilhe sua chave de API em locais públicos ou acessíveis por terceiros.

## Como autenticar uma requisição à API

Para autenticar uma requisição, inclua sua chave de API no cabeçalho `X-CREDIPAY-API-KEY`.

A sua chave de API staging funcionará **somente** para chamadas com o URL [https://api.pre.credix.finance](https://api.pre.credix.finance) (feito para testes). Este ambiente não gera nenhum tipo de impacto financeiro.

### Exemplo de requisição

```bash
curl --request GET \
--url https://api.pre.credix.finance/v2/buyers?taxId=70631413000079 \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'X-CREDIPAY-API-KEY: SUA_CHAVE_DE_API'

 
```

```json
{
  "data": [
    {
      "id": "a0eebc4b-1f3d-4b2a-8c5f-7e6d5f8e9b2f",
      "taxId": "70631413000079",
      "availableCreditLimitAmountCents": 100000,
      "creditLimitAmountCents": 100000,
      "eligible": true,
      "maxPaymentTermDays": 0,
      "name": "Acme LTDA",
      "onboarded": true
    }
  ],
  "page": 1,
  "items": 1,
  "total": 1
}
```

<br />

# Chave de API - Produção

Antes de criar sua chave de API de produção, a equipe da CrediPay irá realizar alguns testes de integração para validar se está funcionalmente correta. Estes testes são customizados para cada integrador, e serão compartilhados ao longo do processo de desenvolvimento. 

Com a chave de API de produção, você poderá realizar chamadas para a URL [https://api.credix.finance](https://api.credix.finance). Neste ambiente, os dados transacionados terão impacto financeiro
