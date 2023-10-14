FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["VacancyImportService/VacancyImportService.csproj", "VacancyImportService/"]
RUN dotnet restore "VacancyImportService/VacancyImportService.csproj"
COPY . .
WORKDIR "/src/VacancyImportService"
RUN dotnet build "VacancyImportService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "VacancyImportService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VacancyImportService.dll"]
