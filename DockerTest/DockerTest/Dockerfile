FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY DockerTest/DockerTest.csproj DockerTest/
RUN dotnet restore DockerTest/DockerTest.csproj
COPY . .
WORKDIR /src/DockerTest
RUN dotnet build DockerTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerTest.dll"]
