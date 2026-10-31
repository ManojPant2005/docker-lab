# Dotnet Web API + SQL Server with Docker

Run a .NET 8 Web API and SQL Server 2022 together using Docker. No need to install SQL Server locally.

## Prerequisites
- Docker Desktop (Engine Running)
- .NET 8 SDK (only for local development, not needed inside Docker)

## Project Structure

MyDotnetApp/
├── MyApi/                  # Your .NET Web API project
│   ├── Program.cs          # App entry point
│   ├── appsettings.json    # Config (ConnectionStrings)
│   └── MyApi.csproj        # Project definition -> MUST be net8.0
├── Dockerfile              # Recipe to build API image (multi-stage)
├── docker-compose.yml      # Recipe to run API + SQL Server together
├── .dockerignore           # Files to ignore while building
└── README.md

### What each Docker file does

**1. Dockerfile (How to build ONE image)**
```dockerfile
# Stage 1: Build with SDK (big image, has compiler)
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
COPY MyApi/*.csproj -> restore
COPY . . -> publish

# Stage 2: Run with ASP.NET Runtime (small image, only runtime)
FROM mcr.microsoft.com/dotnet/aspnet:8.0
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "MyApi.dll"]
