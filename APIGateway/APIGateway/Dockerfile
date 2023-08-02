
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debug

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

EXPOSE 80


COPY ["APIGateway/APIGateway/APIGateway.csproj", "."]
RUN dotnet restore


COPY APIGateway/APIGateway/ .
RUN dotnet publish "APIGateway.csproj" -c Release -o out


FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "APIGateway.dll"]
