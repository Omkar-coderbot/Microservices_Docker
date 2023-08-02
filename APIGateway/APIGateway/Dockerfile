
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debug


# Stage 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src

# Copy the .csproj file and restore dependencies
COPY APIGateway/APIGateway/APIGateway.csproj APIGateway/
RUN dotnet restore APIGateway/APIGateway.csproj

# Copy the entire application code and build
COPY . APIGateway/
WORKDIR /src/APIGateway/
RUN dotnet build -c Release -o /app/build

# Publish the application
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Create the final runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS final
WORKDIR /app

# Copy the published files from the build stage
COPY --from=build /app/publish .

# Expose the port the application will listen on
EXPOSE 80

# Set the entry point for the container
ENTRYPOINT ["dotnet", "APIGateway.dll"]







# FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
# WORKDIR /app

# EXPOSE 80


# COPY ["APIGateway/APIGateway/APIGateway.csproj", "."]
# RUN dotnet restore


# COPY APIGateway/APIGateway/ .
# RUN dotnet publish "APIGateway.csproj" -c Release -o out


# FROM mcr.microsoft.com/dotnet/aspnet:6.0
# WORKDIR /app
# COPY --from=build /app/out .
# ENTRYPOINT ["dotnet", "APIGateway.dll"]
