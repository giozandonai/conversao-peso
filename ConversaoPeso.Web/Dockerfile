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

# FROM mcr.microsoft.com/dotnet/sdk:5.0 as build-env
# WORKDIR /app

# COPY ConversaoPeso.Web.csproj .
# RUN dotnet restore "ConversaoPeso.Web.csproj"

# COPY . .
# RUN dotnet publish "ConversaoPeso.Web.csproj" -c Release -o publish

# FROM mcr.microsoft.com/dotnet/aspnet:5.0
# WORKDIR /app
# EXPOSE 8080
# COPY --from=build-env /app/publish .
# ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]