# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

COPY *.sln .
COPY SpotAcademy.API/*.csproj ./SpotAcademy.API/
RUN dotnet restore

COPY SpotAcademy.API/. ./SpotAcademy.API/
WORKDIR /app/SpotAcademy.API
RUN dotnet publish -c Release -o out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/SpotAcademy.API/out ./
ENTRYPOINT ["dotnet", "SpotAcademy.API.dll"]
