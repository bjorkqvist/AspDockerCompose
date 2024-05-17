FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["AspDockerCompose.App1/AspDockerCompose.App1.csproj", "AspDockerCompose.App1/"]
RUN dotnet restore "AspDockerCompose.App1/AspDockerCompose.App1.csproj"
COPY . .
WORKDIR "/src/AspDockerCompose.App1"
RUN dotnet build "AspDockerCompose.App1.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "AspDockerCompose.App1.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AspDockerCompose.App1.dll"]
