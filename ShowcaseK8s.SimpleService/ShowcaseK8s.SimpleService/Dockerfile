#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["ShowcaseK8s.SimpleService/ShowcaseK8s.SimpleService.csproj", "ShowcaseK8s.SimpleService/"]
RUN dotnet restore "ShowcaseK8s.SimpleService/ShowcaseK8s.SimpleService.csproj"
COPY . .
WORKDIR "/src/ShowcaseK8s.SimpleService"
RUN dotnet build "ShowcaseK8s.SimpleService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ShowcaseK8s.SimpleService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ShowcaseK8s.SimpleService.dll"]