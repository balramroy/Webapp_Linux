#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Webapp_Linux/Webapp_Linux.csproj", "Webapp_Linux/"]
RUN dotnet restore "Webapp_Linux/Webapp_Linux.csproj"
COPY . .
WORKDIR "/src/Webapp_Linux"
RUN dotnet build "Webapp_Linux.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Webapp_Linux.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Webapp_Linux.dll"]