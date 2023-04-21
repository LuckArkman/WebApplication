FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["VeicleAPI/VeicleAPI.csproj", "VeicleAPI/"]
RUN dotnet restore "VeicleAPI/VeicleAPI.csproj"
COPY . .
WORKDIR "/src/VeicleAPI"
RUN dotnet build "VeicleAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "VeicleAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VeicleAPI.dll"]
