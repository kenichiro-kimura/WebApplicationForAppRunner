#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["WebApplicationForAppRunner/WebApplicationForAppRunner.csproj", "WebApplicationForAppRunner/"]
RUN dotnet restore "WebApplicationForAppRunner/WebApplicationForAppRunner.csproj"
COPY . .
WORKDIR "/src/WebApplicationForAppRunner"
RUN dotnet build "WebApplicationForAppRunner.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplicationForAppRunner.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplicationForAppRunner.dll"]