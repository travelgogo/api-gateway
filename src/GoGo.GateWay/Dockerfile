FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 7000

ENV ASPNETCORE_URLS=http://+:7000

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/GoGo.GateWay/GoGo.GateWay.csproj", "src/GoGo.GateWay/"]
RUN dotnet restore "src\GoGo.GateWay\GoGo.GateWay.csproj"
COPY . .
WORKDIR "/src/src/GoGo.GateWay"
RUN dotnet build "GoGo.GateWay.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GoGo.GateWay.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GoGo.GateWay.dll"]
