# Usa l'immagine di .NET SDK 8.0 per costruire l'app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copia il file di progetto e ripristina i pacchetti
COPY ArduinoGymAccess.Web.csproj .
RUN dotnet restore

# Copia tutto il resto e costruisci l'app
COPY . .
RUN dotnet publish -c Release -o /publish

# Usa un server Nginx per servire i file statici di Blazor
FROM nginx:latest AS runtime
COPY --from=build /publish/wwwroot /usr/share/nginx/html
EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]
