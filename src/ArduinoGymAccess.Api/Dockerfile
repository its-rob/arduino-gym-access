# Usa l'immagine di .NET SDK 8.0 per costruire l'app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copia il file di progetto specifico del backend e ripristina i pacchetti
COPY ArduinoGymAccess.Api.csproj .
RUN dotnet restore

# Copia tutto il resto e costruisci l'app
COPY . .
RUN dotnet publish -c Release -o /publish

# Usa l'immagine di runtime di .NET 8.0 per eseguire l'app
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /publish
COPY --from=build /publish .
EXPOSE 80

ENTRYPOINT ["dotnet", "ArduinoGymAccess.Api.dll"]
