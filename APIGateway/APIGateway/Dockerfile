
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debug




FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

COPY ["APIGateway/APIGateway/APIGateway.csproj", "."]
RUN dotnet restore


COPY APIGateway/APIGateway/ .
RUN dotnet publish "APIGateway.csproj" -c Release -o publish


FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/publish .


EXPOSE 80
ENTRYPOINT ["dotnet", "APIGateway.dll"]
