FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["Microservices.Kubernetes/Microservices.Kubernetes.csproj", "Microservices.Kubernetes/"]

RUN dotnet restore "Microservices.Kubernetes/Microservices.Kubernetes.csproj"
COPY . .
WORKDIR "/src/Microservices.Kubernetes"
RUN dotnet build "Microservices.Kubernetes.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Microservices.Kubernetes.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Microservices.Kubernetes.dll"]