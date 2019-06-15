FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Microservices.Api/Microservices.Api.csproj", "Microservices.Api/"]
RUN dotnet restore "Microservices.Api/Microservices.Api.csproj"
COPY . .
WORKDIR "/src/Microservices.Api"
RUN dotnet build "Microservices.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Microservices.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Microservices.Api.dll"]