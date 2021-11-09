#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DungeonMastersCompanion.FrontEnd/DungeonMastersCompanion.FrontEnd.csproj", "DungeonMastersCompanion.FrontEnd/"]
RUN dotnet restore "DungeonMastersCompanion.FrontEnd/DungeonMastersCompanion.FrontEnd.csproj"
COPY . .
WORKDIR "/src/DungeonMastersCompanion.FrontEnd"
RUN dotnet build "DungeonMastersCompanion.FrontEnd.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DungeonMastersCompanion.FrontEnd.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DungeonMastersCompanion.FrontEnd.dll"]