
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debug

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

EXPOSE 80

# copy project csproj file and restore it in docker directory
COPY ["APIGateway/APIGateway/APIGateway.csproj", "."]
RUN dotnet restore

# Copy everything into the docker directory and build
COPY APIGateway/APIGateway/ .
RUN dotnet publish "APIGateway.csproj" -c Release -o out

# Build runtime final image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "APIGateway.dll"]
