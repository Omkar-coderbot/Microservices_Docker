#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.



FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build


WORKDIR /app


COPY ["UserService/UserService.csproj", "."]
RUN dotnet restore


COPY UserService/ .
RUN dotnet publish "UserService.csproj" -c Release -o publish


FROM mcr.microsoft.com/dotnet/aspnet:6.0

WORKDIR /app


COPY --from=build /app/publish .

EXPOSE 80
ENTRYPOINT ["dotnet", "UserService.dll"]
