#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["A5E-Orchestrator/A5E-Orchestrator.csproj", "A5E-Orchestrator/"]
RUN dotnet restore "A5E-Orchestrator/A5E-Orchestrator.csproj"
COPY . .
WORKDIR "/src/A5E-Orchestrator"
RUN dotnet build "A5E-Orchestrator.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "A5E-Orchestrator.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "A5E-Orchestrator.dll"]