# <img src="https://cdn.iconscout.com/icon/free/png-256/microsoft-dot-net-1175176.png" height=30 width=30> Como configurar ambiente para usar a SDK Mercado Pago .NET

## 1. Para uso da SDK .NET é necessária a instalação dos seguintes itens:

* .NET Standard 2.0+
* .NET Core 2.0+
* .NET Framework 4.6.1+.

## 2. Clone o SDK.

```
git clone git@github.com:mercadopago/sdk-dotnet.git
```

## 3. Abra o projeto baixado com sua IDE preferida.

> Sugestão: Visual Studio ou VSCode.

## 4. Na raiz do projeto, crie uma pasta "samples" e inicie um projeto .NET.

Para iniciar um projeto dotnet, dentro da pasta "samples" digite:

```
dotnet new console
```

## 5. Após criado o projeto, modifique o arquivo "samples.csproj".

Dentro do arquivo, insira o trecho abaixo que será responsável por mapeado nossa SDK local para o nosso projeto "samples".

```xml
  <ItemGroup>
    <ProjectReference Include="..\src\MercadoPago\MercadoPago.csproj" />
  </ItemGroup>
```

O arquivo ficará assim:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <ProjectReference Include="..\src\MercadoPago\MercadoPago.csproj" />
  </ItemGroup>

</Project>

```

## 6. Dentro do arquivo "Program.cs", copie e cole o snipet abaixo:

```dotnet
using System;
using MercadoPago.Config;
using MercadoPago.Client.Common;
using MercadoPago.Client.Payment;
using MercadoPago.Resource.Payment;

MercadoPagoConfig.AccessToken = "ENV_ACCESS_TOKEN";

var request = new PaymentCreateRequest
{
    TransactionAmount = 105,
    Description = "Título do produto",
    PaymentMethodId = "pix",
    Payer = new PaymentPayerRequest
    {
        Email = "test_user_24634097@testuser.com",
        FirstName = "Test",
        LastName = "User",
        Identification = new IdentificationRequest
        {
            Type = "CPF",
            Number = "191191191-00",
        },
    },
};

var client = new PaymentClient();
Payment payment = await client.CreateAsync(request);

Console.WriteLine(Newtonsoft.Json.JsonConvert.SerializeObject(payment));
```
> Substitua "ENV_ACCESS_TOKEN" pelo access token da [sua aplicação](https://www.mercadopago.com.br/developers/panel).

> O e-mail deve ser um email de teste válido.

> O snipet assima é apenas um exemplo, consulte nossa [documentação oficial](https://www.mercadopago.com.br/developers/pt/guides) para mais informações.

## 7. Execute o projeto e verifique o resultado.

Na pasta "samples", digite:
```
dotnet run
```
Caso tenha resposta da API o ambiente está devidamente configurado, caso contrário, refaça os passos e tente novamente. 