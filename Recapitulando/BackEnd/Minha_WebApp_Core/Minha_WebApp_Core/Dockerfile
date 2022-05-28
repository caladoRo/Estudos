#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Minha_WebApp_Core/Minha_WebApp_Core.csproj", "Minha_WebApp_Core/"]
RUN dotnet restore "Minha_WebApp_Core/Minha_WebApp_Core.csproj"
COPY . .
WORKDIR "/src/Minha_WebApp_Core"
RUN dotnet build "Minha_WebApp_Core.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Minha_WebApp_Core.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Minha_WebApp_Core.dll"]