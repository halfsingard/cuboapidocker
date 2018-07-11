FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY CuboApiDocker/CuboApiDocker.csproj CuboApiDocker/
RUN dotnet restore CuboApiDocker/CuboApiDocker.csproj
COPY . .
WORKDIR /src/CuboApiDocker
RUN dotnet build CuboApiDocker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish CuboApiDocker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CuboApiDocker.dll"]
