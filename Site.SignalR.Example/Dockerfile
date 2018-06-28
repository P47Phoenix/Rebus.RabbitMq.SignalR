FROM microsoft/dotnet:2.1-aspnetcore-runtime-bionic-arm32v7 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY / /
run ls
RUN dotnet restore ./Rebus.RabbitMq.SignalR.sln
WORKDIR /src
RUN dotnet build ./Site.SignalR.Example/Site.SignalR.Example.csproj -c Release -o /app
FROM build AS publish
WORKDIR /src/Site.SignalR.Example
RUN dotnet publish ./Site.SignalR.Example.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Site.SignalR.Example.dll"]
