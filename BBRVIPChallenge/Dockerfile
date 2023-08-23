FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BBRVIPChallenge/BBRVIPChallenge.csproj", "BBRVIPChallenge/"]
RUN dotnet restore "BBRVIPChallenge/BBRVIPChallenge.csproj"
COPY . .
WORKDIR "/src/BBRVIPChallenge"
RUN dotnet build "BBRVIPChallenge.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BBRVIPChallenge.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BBRVIPChallenge.dll"]
