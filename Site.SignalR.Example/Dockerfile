FROM microsoft/dotnet:2.1-aspnetcore-runtime-bionic-arm32v7 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Site.SignalR.Example/Site.SignalR.Example.csproj Site.SignalR.Example/
RUN dotnet restore Site.SignalR.Example/Site.SignalR.Example.csproj
COPY . .
WORKDIR /src/Site.SignalR.Example
FROM build AS publish
RUN dotnet publish Site.SignalR.Example.csproj -c Release -o /app -r linux-arm

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Site.SignalR.Example.dll"]
