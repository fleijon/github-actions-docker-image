# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY "./src/Sample/Sample.csproj" "src/Sample/"
RUN dotnet restore "src/Sample/Sample.csproj"

# Copy everything else and build
COPY . .
RUN dotnet publish "/app/src/Sample/Sample.csproj" -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "Sample.dll"]