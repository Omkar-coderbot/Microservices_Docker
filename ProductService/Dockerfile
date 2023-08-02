
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.


# FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
# WORKDIR /app

# EXPOSE 80

# # copy project csproj file and restore it in docker directory
# COPY ["Microservices_Docker/ProjectService/ProjectService.csproj", "."]
# RUN dotnet restore

# # Copy everything into the docker directory and build
# COPY Microservicee_Docker/ProjectService/ .
# RUN dotnet publish "ProjectService.csproj" -c Release -o out

# # Build runtime final image
# FROM mcr.microsoft.com/dotnet/aspnet:6.0
# WORKDIR /app
# COPY --from=build /app/out .
# ENTRYPOINT ["dotnet", "ProjectService.dll"]


FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

EXPOSE 80

COPY ["ProductService/ProductService.csproj", "."]
RUN dotnet restore


COPY ProductService/ .
RUN dotnet publish "ProductService.csproj" -c Release -o out
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "ProductService.dll"]
