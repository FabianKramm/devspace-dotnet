FROM mcr.microsoft.com/dotnet/core/sdk:2.1 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY ./hello-world-api/*.csproj ./hello-world-api/

RUN dotnet restore "hello-world-api/hello-world-api.csproj"

# copy everything else and build app
COPY hello-world-api/. ./hello-world-api

WORKDIR /app/hello-world-api
RUN dotnet publish -c Debug -o bin

EXPOSE 5004

################ Production ################
# Creates a minimal image for production using a different base image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.1 as production

# Create project directory (workdir)
WORKDIR /app

# Copy application binary from build/dev stage to the distroless container
COPY --from=build /app/bin .

# Container start command for production (ADJUST DLL NAME TO YOUR PROJECT)
CMD ["dotnet", "hello-world-api.dll"]
