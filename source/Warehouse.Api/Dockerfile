FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["source/Warehouse.Api/Warehouse.Api.csproj", "source/Warehouse.Api/"]
RUN dotnet restore "source/Warehouse.Api/Warehouse.Api.csproj"
COPY . .
WORKDIR "/src/source/Warehouse.Api"
RUN dotnet build "Warehouse.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Warehouse.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Warehouse.Api.dll"]