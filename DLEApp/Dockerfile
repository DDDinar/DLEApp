FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DLEApp/DLEApp.csproj", "DLEApp/"]
RUN dotnet restore "DLEApp/DLEApp.csproj"
COPY . .
WORKDIR "/src/DLEApp"
RUN dotnet build "DLEApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DLEApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DLEApp.dll"]
