# <img src="https://edent.github.io/SuperTinyIcons/images/svg/ruby.svg" height=30 width=30> Como configurar ambiente para usar a SDK Mercado Pago Ruby

## 1. Verifique se o a versão do Ruby instalada é a 2.3 ou superior.

```
ruby -v
```

## 2. Clone o SDK.

```
git clone git@github.com:mercadopago/sdk-ruby.git
```

## 3. Abra o projeto baixado com sua IDE preferida.

> Sugestão: VSCode.

## 4. Instale as dependências do projeto.

No terminal, dentro do projeto, digite: 
```
bundle install
```

## 5. Na raiz do projeto, crie uma pasta "samples".

## 6. Dentro da pasta "samples" crie um arquivo para ser seu arquivo de testes.

> Exemplo: payment.rb

## 7. Dentro do arquivo, copie e cole o snipet abaixo:

```ruby
require './lib/mercadopago.rb'
sdk = Mercadopago::SDK.new('ENV_ACCESS_TOKEN')

payment_request = {
  transaction_amount: 100,
  description: 'Título do produto',
  payment_method_id: 'pix',
  payer: {
    email: 'test_user_24634097@testuser.com',
    identification: {
      type: 'CPF',
      number: '19119119100',
    }
  }
}

payment_response = sdk.payment.create(payment_request)
payment = payment_response[:response]

print payment
```
> Substitua "ENV_ACCESS_TOKEN" pelo access token da [sua aplicação](https://www.mercadopago.com.br/developers/panel).

> O e-mail deve ser um email de teste válido.

> O snipet assima é apenas um exemplo, consulte nossa [documentação oficial](https://www.mercadopago.com.br/developers/pt/guides) para mais informações.

## 8. Execute o arquivo e verifique o resultado.

```
ruby samples/payment.rb
```
Caso tenha resposta da API o ambiente está devidamente configurado, caso contrário, refaça os passos e tente novamente. 