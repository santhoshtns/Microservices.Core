FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["Microservices.Web/Microservices.Web.csproj", "Microservices.Web/"]

RUN dotnet restore "Microservices.Web/Microservices.Web.csproj"
COPY . .
WORKDIR "/src/Microservices.Web"
RUN dotnet build "Microservices.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Microservices.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Microservices.Web.dll"]