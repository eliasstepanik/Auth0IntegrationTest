FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Auth0IntegrationTest/Auth0IntegrationTest.csproj", "Auth0IntegrationTest/"]
RUN dotnet restore "Auth0IntegrationTest/Auth0IntegrationTest.csproj"
COPY . .
WORKDIR "/src/Auth0IntegrationTest"
RUN dotnet build "Auth0IntegrationTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Auth0IntegrationTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Auth0IntegrationTest.dll"]
