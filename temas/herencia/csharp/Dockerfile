# Utiliser l'image .NET SDK pour construire le projet
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Définir le répertoire de travail à l'intérieur du conteneur
WORKDIR /src

# Copier les fichiers .csproj et restaurer les dépendances
COPY mainproject.csproj ./
RUN dotnet restore

# Copier le reste du code source et construire le projet
COPY . .
RUN dotnet publish -c Release -o /app

# Utiliser l'image .NET Runtime pour exécuter l'application
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app .

# Spécifier la commande à exécuter lorsque le conteneur démarre
ENTRYPOINT ["dotnet", "mainproject.dll"]