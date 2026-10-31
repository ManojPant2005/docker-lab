# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY TestWebApi/*.csproj ./TestWebApi/
RUN dotnet restore ./TestWebApi/TestWebApi.csproj
COPY . .
WORKDIR /src/TestWebApi
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Run
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 80
EXPOSE 443
ENTRYPOINT ["dotnet", "TestWebApi.dll"]
