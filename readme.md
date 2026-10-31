MyDotnetApp/
├── MyApi/                  -> dotnet web api project
│   ├── Program.cs
│   ├── appsettings.json
│   └── MyApi.csproj
├── Dockerfile              -> How to build API image
├── docker-compose.yml      -> How to run API + SQL Server together
├── .dockerignore
└── README.md

# Build both images and start both containers
docker-compose up --build

# Now check:
# API: http://localhost:5000/swagger
# SQL: You can connect in SSMS with localhost,1433 / sa / YourStrong@Pass123

# See logs live
docker-compose logs -f
docker-compose logs -f api
docker-compose logs -f db

# Stop (pause, data safe in sqlserver_data volume)
docker-compose stop

# Start again (fast, no build)
docker-compose start

# Restart (when you change code)
docker-compose restart
docker-compose restart api

# Full shutdown (deletes containers, but data volume stays safe)
docker-compose down

# Full delete including data (DANGEROUS - deletes your DB)
docker-compose down -v