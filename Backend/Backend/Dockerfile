# -------------------------
# Build stage
# -------------------------
FROM mcr.microsoft.com/dotnet/sdk:8.0-alpine AS build
WORKDIR /src

# Copy csproj and restore
COPY Backend/*.csproj Backend/
RUN dotnet restore Backend/Backend.csproj

# Copy everything else
COPY . .
WORKDIR /src/Backend
RUN dotnet publish -c Release -o /app/publish

# -------------------------
# Runtime stage
# -------------------------
FROM mcr.microsoft.com/dotnet/aspnet:8.0-alpine
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Backend.dll"]
