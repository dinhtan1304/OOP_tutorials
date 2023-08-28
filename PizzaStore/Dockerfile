FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["PizzaStore/PizzaStore.csproj", "PizzaStore/"]
RUN dotnet restore "PizzaStore/PizzaStore.csproj"
COPY . .
WORKDIR "/src/PizzaStore"
RUN dotnet build "PizzaStore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PizzaStore.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PizzaStore.dll"]
