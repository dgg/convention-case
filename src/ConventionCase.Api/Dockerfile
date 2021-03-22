FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 5000
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/ConventionCase.Api/ConventionCase.Api.csproj", "src/ConventionCase.Api/"]
RUN dotnet restore "src/ConventionCase.Api/ConventionCase.Api.csproj"
COPY . .
WORKDIR "/src/src/ConventionCase.Api"
RUN dotnet build "ConventionCase.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ConventionCase.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ConventionCase.Api.dll"]
