# <img src="https://edent.github.io/SuperTinyIcons/images/svg/php.svg" height=30 width=30> Como configurar ambiente para usar a SDK Mercado Pago PHP v2

## 1. Verifique se a versão do PHP instalada é a 7.1 ou superior.

```
php -v
```

Caso não tenha instalado, sugerimos a instalação via HomeBrew com o comando: 

```
brew install php@7.3
```

Após a instalação rodar o comando abaixo e verificar novamente se a versão foi alterada.

```
brew link --overwrite --force php@7.3
```
ou
```
brew unlink php && brew link --overwrite --force php@7.3
```

## 2. Instale o Composer.

[Clique aqui](https://getcomposer.org/doc/00-intro.md) para instalar o Composer.

Após instalado, execute o comando abaixo para verificar se a instalação foi bem sucedida.

```
composer -v
```

## 3. Clone o SDK.

```
git clone git@github.com:mercadopago/sdk-php.git
```

## 4. Abra o projeto baixado com sua IDE preferida.

> Sugestão: VSCode.

## 5. Para usar a v2 deve-se mudar para a branch "master".

```
git checkout master
```

## 6. Instale as dependências do projeto.

No terminal, na raiz do projeto, digite: 
```
composer install
```

## 7. Na raiz do projeto, acesse a pasta "samples" e altere o arquivo composer.json.

Insira as informações abaixo no composer.json, após isso, dentro da pasta samples, instale as dependencias da pasta samples.

```json
{
  "repositories": [
      {
          "type": "path",
          "url": "../../sdk-php"
      }
  ],
  "require": {
      "mercadopago/dx-php": "@dev"
  }
}
```

> Isso fará com que ao executar seus samples eles estarão utilizando seu sdk local.

## 8. Crie um arquivo para ser seu arquivo de testes dentro da pasta "samples".

> Exemplo: payment.php

> Você também pode usar o código já existentes dentro de "samples" desde com as devidas modificações necessárias.

## 9. Dentro do arquivo, copie e cole o snipet abaixo:

```php
<?php
 require_once 'vendor/autoload.php';

 MercadoPago\SDK::setAccessToken("ENV_ACCESS_TOKEN");

 $payment = new MercadoPago\Payment();
 $payment->transaction_amount = 100;
 $payment->description = "Título do produto";
 $payment->payment_method_id = "pix";
 $payment->payer = array(
     "email" => "test_user_24634097@testuser.com",
     "first_name" => "Test",
     "last_name" => "User",
     "identification" => array(
         "type" => "CPF",
         "number" => "19119119100"
      ),
     "address"=>  array(
         "zip_code" => "06233200",
         "street_name" => "Av. das Nações Unidas",
         "street_number" => "3003",
         "neighborhood" => "Bonfim",
         "city" => "Osasco",
         "federal_unit" => "SP"
      )
   );

 $payment->save();

 var_dump($payment)

?>
```
> Substitua "ENV_ACCESS_TOKEN" pelo access token da [sua aplicação](https://www.mercadopago.com.br/developers/panel).

> O e-mail deve ser um email de teste válido.

> O snipet assima é apenas um exemplo, consulte nossa [documentação oficial](https://www.mercadopago.com.br/developers/pt/guides) para mais informações.

## 10. Execute o arquivo e verifique o resultado.

```
php samples/payment.php
```
Caso tenha resposta da API o ambiente está devidamente configurado, caso contrário, refaça os passos e tente novamente. 
