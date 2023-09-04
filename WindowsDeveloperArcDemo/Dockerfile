FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WindowsDeveloperArcDemo/WindowsDeveloperArcDemo.csproj", "WindowsDeveloperArcDemo/"]
RUN dotnet restore "WindowsDeveloperArcDemo/WindowsDeveloperArcDemo.csproj"
COPY . .
WORKDIR "/src/WindowsDeveloperArcDemo"
RUN dotnet build "WindowsDeveloperArcDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WindowsDeveloperArcDemo.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WindowsDeveloperArcDemo.dll"]