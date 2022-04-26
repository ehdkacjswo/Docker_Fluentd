FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 5000
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["APIServer/ApiServer.csproj", "APIServer/"]
RUN dotnet restore "APIServer/ApiServer.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "APIServer/ApiServer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "APIServer/ApiServer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ApiServer.dll"]
