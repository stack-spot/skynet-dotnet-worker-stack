No processo de conectar softwares de uma empresa através de um Worker, a Stack oferece velocidade e confiança para times de desenvolvimento.

Ao iniciar o seu produto através do template base oferecido, é possível compilar e executar o projeto localmente. É importante lembrar que a Stack não é intrusiva. Os códigos são criados para ajudar times de desenvolvimento, mas cada desenvolvedor opta pelo que prefere usar.   

Para começar sua jornada de desenvolvimento utilizando os recursos disponibilizados pelo Estúdio Skynet, aplique o template base para iniciar o desenvolvimento de um Worker completo usando **C#**, **.NET** e **REST**, rodando em um cluster de contêiner. 

### Visão Geral
O template **worker-app-cs-template** adiciona em uma stack a capacidade de provisionar serviços que executam em background.

### Pré-requisitos
Para utilizar esse template você precisa utilizar o `CLI` do `StackSpot` que você pode baixar [**aqui**](https://stackspot.com.br/).
- .NET 5 e/ou 6 instalados.
- Ao criar sua pipeline da AWS **e não encontrar no campo "Runtime" a opção do dotnet: 5.0**, siga as orientações descritas neste [**link**](https://confluence-itau.tecnologia.prod.ops.aws.cloud.ihf/x/GDaYJ).

### Inputs
Os inputs necessários para utilizar o template são:
| **Campo** | **Valor** | **Descrição** |
| :--- | :--- | :--- |
| Project Name| ex.: MyApp | Nome da aplicação  |
| Target Framework| 5 ou 6 | Framework em que o Worker será criado  |

## Execução do projeto criado

Após criar o projeto, acesse o diretório onde se encontra a `Solution` e os demais arquivos do projeto. Despois disso, execute o seguinte comando:

```bash
    dotnet restore <meu App>.Worker.sln
```

Realize também a compilação do projeto, através do comando abaixo:

```bash
    dotnet build <meu App>.Worker.sln
```

Realize a execução dos testes unitários e de integração. Execute o seguinte comando:

```bash
dotnet test <meu App>.Worker.sln
```

Para testar a aplicação, ainda no mesmo diretório da `Solution`. Execute o seguinte comando:

```bash
    dotnet run --project ./src/<meu App>.Worker/<meu App>.Worker.csproj
```

### Configuração do Docker

Para que o Docker funcione, você precisará adicionar um certificado SSL temporário e montar um volume para manter esse certificado.
Você pode encontrar no [**Microsoft Docs**](https://docs.microsoft.com/en-us/aspnet/core/security/docker-https?view=aspnetcore-6.0) que descrevem as etapas necessárias para **Windows**, **macOS** e **Linux**.

- Para Windows:
O seguinte precisará ser executado a partir do seu terminal para criar um certificado:

```bash
dotnet dev-certs https -ep %USERPROFILE%\.aspnet\https\aspnetapp.pfx -p Your_password123
dotnet dev-certs https --trust
```

NOTA: Ao usar o PowerShell, substitua **%USERPROFILE%** por **$env:USERPROFILE**.

- Para macOS:
```bash
dotnet dev-certs https -ep ${HOME}/.aspnet/https/aspnetapp.pfx -p Your_password123
dotnet dev-certs https --trust
```

- Para Linux:
```bash
dotnet dev-certs https -ep ${HOME}/.aspnet/https/aspnetapp.pfx -p Your_password123
dotnet dev-certs https --trust
```

1. Para construir e executar os containers Docker, execute o comando abaixo na raiz da solução onde você encontra o arquivo **`docker-compose.yml`**:

 ```bash
 docker-compose -f 'docker-compose.yml' up --build
 ```

2. Em seguida, abra http://localhost:5000/health no seu navegador.

> Dica: Você também pode utilizar uma IDE (VSCode, Visual Studio) de sua preferência para realizar os passos acima.

Aplicando este projeto base, é possível adicionar as seguintes capacidades ao seu template base:

#### Logging  
 Se você possui vários projetos, micro serviços e ou rotinas, com esse plugin você conseguirá manter a qualidade e padrão de informações de log para todas elas, considerando diferentes níveis de log.  Isso permite definir Tags para que você consiga quantificar e/ou classificar erros, trazendo uma visão de falhas recorrentes ou permitindo a prevenção de problemas futuros. 
 Além disso, é fácil fazer a integração com ferramentas como Splunk ou AWS Cloud Watch para monitorar e visualizar os dados, garantindo observabilidade de suas aplicações.

#### Metrics  
O plugin de Metrics facilita a medição da quantidade de requisições em um endpoint crítico ou o monitoramento do tamanho de payloads que são enviados para sua API.

#### Trace  
Já o plugin de Trace facilita a instrumentação de telemetria da sua API, através do Opentelemetry com exporter para Jaeger e AWS X-Ray. 

#### Queue  
O plugin Queue simplifica toda a configuração e implementação de um ambiente descentralizado, voltado à micro serviços e que se comunicam entre si, utilizando filas de mensagens. Comparado a criar uma classe, o plugin Queue consegue abstrair toda a complexidade para a comunicação com a sua fila AWS SQS.

#### Secrets  
O plugin Secrets facilita o gerenciamento de informações sensíveis de sistemas com chaves de APIs, tokens de autenticação ou conexões com bases de dados. Tendo em vista a utilização de um Secret Manager como o da AWS, essa gestão ficará mais fácil, pois o plugin simplifica o consumo dessas informações. Utilize o plugin Secrets a qualquer momento em que você desejar dentro da sua aplicação. 

#### Bucket  
Manipule arquivos utilizando o plugin Bucket, esse plugin elimina a complexidade e facilita a instrumentação com a Amazon Simple Storage Service (S3).

#### Repository  
Armazene dados ou documentos de forma trivial, o plugin Repository reúne todas as capacidades do AWS DynamoDB de forma simples e rápida.

Ao fim do ciclo de desenvolvimento, utilizando todas as capacidades que nossa Stack oferece, é possível ter uma estrutura completa como ilustra a imagem abaixo:

![Caso de Uso](https://raw.githubusercontent.com/stack-spot/skynet-dotnet-stack/main/use-case.png "Caso de Uso")

Veja mais detalhes de cada plugin, casos e formas de uso disponíveis através do menu lateral esquerdo. 
