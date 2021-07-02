#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["acme.sistemas.obra.api/acme.sistemas.obra.api.csproj", "acme.sistemas.obra.api/"]
RUN dotnet restore "acme.sistemas.obra.api/acme.sistemas.obra.api.csproj"
COPY . .
WORKDIR "/src/acme.sistemas.obra.api"
RUN dotnet build "acme.sistemas.obra.api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "acme.sistemas.obra.api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "acme.sistemas.obra.api.dll"]