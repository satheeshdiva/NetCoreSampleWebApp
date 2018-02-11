FROM microsoft/aspnetcore:2.0-nanoserver-sac2016 AS base
WORKDIR /
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-sac2016 AS build
WORKDIR /
COPY *.sln ./
COPY NetCoreSampleWebApp/NetCoreSampleWebApp.csproj NetCoreSampleWebApp/
RUN dotnet restore
COPY . .
WORKDIR /NetCoreSampleWebApp
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreSampleWebApp.dll"]
