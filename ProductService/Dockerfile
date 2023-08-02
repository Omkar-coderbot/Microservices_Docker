
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.



FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

COPY ["ProductService/ProductService.csproj", "."]
RUN dotnet restore


COPY ProductService/ .
RUN dotnet publish "ProductService.csproj" -c Release -o output
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/output .

EXPOSE 80
ENTRYPOINT ["dotnet", "ProductService.dll"]
