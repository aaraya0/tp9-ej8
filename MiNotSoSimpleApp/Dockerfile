# Usa la imagen oficial de .NET Core
FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

# Usa la imagen oficial de .NET Core SDK para construir la aplicación
FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["tp9-ej8/MiNotSoSimpleApp/MiNotSoSimpleApp.csproj", "tp9-ej8/MiNotSoSimpleApp/"]
RUN dotnet restore "MiNotSoSimpleApp/MiNotSoSimpleApp.csproj"
COPY . .
WORKDIR "/src/MiNotSoSimpleApp"
RUN dotnet build "MiNotSoSimpleApp.csproj" -c Release -o /app/build

# Publica la aplicación
FROM build AS publish
RUN dotnet publish "MiNotSoSimpleApp.csproj" -c Release -o /app/publish

# Usa la imagen base y copia la aplicación publicada
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MiNotSoSimpleApp.dll"]
