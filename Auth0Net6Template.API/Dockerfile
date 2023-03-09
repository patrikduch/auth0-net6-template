#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Auth0Net6Template.API/Auth0Net6Template.API.csproj", "Auth0Net6Template.API/"]
RUN dotnet restore "Auth0Net6Template.API/Auth0Net6Template.API.csproj"
COPY . .
WORKDIR "/src/Auth0Net6Template.API"
RUN dotnet build "Auth0Net6Template.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Auth0Net6Template.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Auth0Net6Template.API.dll"]