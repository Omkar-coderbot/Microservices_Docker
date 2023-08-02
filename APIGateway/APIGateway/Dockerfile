
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debug




# FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
# WORKDIR /app

# COPY ["APIGateway/APIGateway/APIGateway.csproj", "."]
# RUN dotnet restore


# COPY APIGateway/APIGateway/ .
# RUN dotnet publish "APIGateway.csproj" -c Release -o publish


# FROM mcr.microsoft.com/dotnet/aspnet:6.0
# WORKDIR /app
# COPY --from=build /app/publish .


# EXPOSE 80
# ENTRYPOINT ["dotnet", "APIGateway.dll"]




# Use the official .NET Core SDK image as the build environment
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the project file and restore dependencies
RUN pwd
# COPY APIGateway/APIGatway/*.csproj .
COPY ["APIGateway/APIGateway/APIGateway.csproj", "."]
RUN dotnet restore

# Copy the entire project and build the application
COPY . .
# COPY APIGateway/APIGateway/ .
RUN dotnet publish "APIGateway.csproj" -c Release -o publish
# COPY . .
# RUN dotnet publish -c Release -o out

# Use a lighter runtime image for the final build
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime

# Set the working directory inside the container
WORKDIR /app

# Copy the published output from the build container
COPY --from=build /app/out .

# Expose the port the API Gateway will listen on
EXPOSE 80

# Set the entry point for the container to start the API Gateway
ENTRYPOINT ["dotnet", "APIGateway.dll"]

# Set the entry point for the container to start the API Gateway
# ENTRYPOINT ["dotnet", "APIGateway.dll"]

