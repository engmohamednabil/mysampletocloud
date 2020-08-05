FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["MySampleToCloud/MySampleToCloud.csproj", "MySampleToCloud/"]
RUN dotnet restore "MySampleToCloud/MySampleToCloud.csproj"
COPY . .
WORKDIR "/src/MySampleToCloud"
RUN dotnet build "MySampleToCloud.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MySampleToCloud.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MySampleToCloud.dll"]