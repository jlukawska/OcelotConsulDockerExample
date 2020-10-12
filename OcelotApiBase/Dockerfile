#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY "OcelotApiBase/" "OcelotApiBase/"
RUN dotnet restore "OcelotApiBase/OcelotApiBase.csproj"
COPY . .
WORKDIR "/src/OcelotApiBase"
RUN dotnet build "OcelotApiBase.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OcelotApiBase.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OcelotApiBase.dll"]
