FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["TestProjectSgs/TestProjectSgs.csproj", "TestProjectSgs/"]
RUN dotnet restore "TestProjectSgs/TestProjectSgs.csproj"
COPY . .
WORKDIR "/src/TestProjectSgs"
RUN dotnet build "TestProjectSgs.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TestProjectSgs.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestProjectSgs.dll"]