FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["ShopApp/ShopApp.csproj", "ShopApp/"]
RUN dotnet restore "ShopApp/ShopApp.csproj"
COPY . .
WORKDIR "/src/ShopApp"
RUN dotnet build "ShopApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ShopApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ShopApp.dll"]
