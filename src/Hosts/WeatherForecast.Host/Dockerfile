#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["WeatherForecast/WeatherForecast.Host.csproj", "WeatherForecast/"]
RUN dotnet restore "WeatherForecast/WeatherForecast.Host.csproj"
COPY . .
WORKDIR "/src/WeatherForecast"
RUN dotnet build "WeatherForecast.Host.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WeatherForecast.Host.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WeatherForecast.Host.dll"]