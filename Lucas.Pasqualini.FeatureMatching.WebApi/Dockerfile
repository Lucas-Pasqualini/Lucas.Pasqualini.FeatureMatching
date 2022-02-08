FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Lucas.Pasqualini.FeatureMatching.WebApi/Lucas.Pasqualini.FeatureMatching.WebApi.csproj", "Lucas.Pasqualini.FeatureMatching.WebApi/"]
RUN dotnet restore "Lucas.Pasqualini.FeatureMatching.WebApi/Lucas.Pasqualini.FeatureMatching.WebApi.csproj"
COPY . .
WORKDIR "/src/Lucas.Pasqualini.FeatureMatching.WebApi"
RUN dotnet build "Lucas.Pasqualini.FeatureMatching.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Lucas.Pasqualini.FeatureMatching.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Lucas.Pasqualini.FeatureMatching.WebApi.dll"]
