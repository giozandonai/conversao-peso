# Projeto conversão de peso

### Sobre o projeto
O projeto conversão de peso é um projeto desenvolvido em C# com .NET Core 5.0. O projeto tem como objetivo ser um exemplo para a criação de ambiente com containers usando .NET.

### Observações do projeto
A aplicação é exposta usando a porta 80 

**ConversaoPeso.Web/Dockerfile**
```
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 as build
WORKDIR /src
COPY ConversaoPeso.Web.csproj .
RUN dotnet restore "ConversaoPeso.Web.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "ConversaoPeso.Web.csproj" -c Release -o /app/build/

FROM build AS publish
RUN dotnet publish "ConversaoPeso.Web.csproj" -c Release -o /app/publish/

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]
```

**Docker Hub - [giozandonai](https://hub.docker.com/u/giozandonai)**

**Criando a imagem sem o compose:** `$ docker build -t giozandonai/conversao-peso:v1 .`

**Enviando imagem:** `$ docker push giozandonai/conversao-peso:v1`

**Adicionando tag latest:** `$ docker tag giozandonai/conversao-peso:v1 conversao-peso:latest`

**Enviando imagem:**
`$ docker push giozandonai/conversao-peso:latest`

**Rodando com o compose:**
`$ docker-compose up -d`

**Rodando com o Docker run:**
`$ docker container run -d --name conversao-peso -p 80:80 giozandonai/conversao-peso:v1`

**Acessando a aplicação:**
`http://localhost`