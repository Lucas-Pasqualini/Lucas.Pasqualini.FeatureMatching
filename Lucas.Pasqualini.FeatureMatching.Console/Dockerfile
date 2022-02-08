FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Lucas.Pasqualini.FeatureMatching.Console/Lucas.Pasqualini.FeatureMatching.Console.csproj", "Lucas.Pasqualini.FeatureMatching.Console/"]
RUN dotnet restore "Lucas.Pasqualini.FeatureMatching.Console/Lucas.Pasqualini.FeatureMatching.Console.csproj"
COPY . .
WORKDIR "/src/Lucas.Pasqualini.FeatureMatching.Console"
RUN dotnet build "Lucas.Pasqualini.FeatureMatching.Console.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Lucas.Pasqualini.FeatureMatching.Console.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Lucas.Pasqualini.FeatureMatching.Console.dll"]
