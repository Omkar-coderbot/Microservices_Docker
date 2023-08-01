#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

# FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
# WORKDIR /app

# FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
# WORKDIR /src
# COPY ["UserService/UserService.csproj", "UserService/"]
# RUN dotnet restore "UserService/UserService.csproj"
# COPY . .
# WORKDIR "/src/UserService"
# RUN dotnet build "UserService.csproj" -c Release -o /app/build

# FROM build AS publish
# RUN dotnet publish "UserService.csproj" -c Release -o /app/publish


# FROM base AS final
# WORKDIR /app
# COPY --from=publish /app/publish .
# EXPOSE 80
# ENTRYPOINT ["dotnet", "UserService.dll"]





FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

EXPOSE 80

# copy project csproj file and restore it in docker directory
COPY ["UserService/UserService.csproj", "."]
RUN dotnet restore

# Copy everything into the docker directory and build
COPY UserService/ .
RUN dotnet publish "UserService.csproj" -c Release -o out

# Build runtime final image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "UserService.dll"]
