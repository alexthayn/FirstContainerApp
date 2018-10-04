FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 59991
EXPOSE 44353

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AlexFirstContainerApp/AlexFirstContainerApp.csproj", "AlexFirstContainerApp/"]
RUN dotnet restore "AlexFirstContainerApp/AlexFirstContainerApp.csproj"
COPY . .
WORKDIR "/src/AlexFirstContainerApp"
RUN dotnet build "AlexFirstContainerApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AlexFirstContainerApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AlexFirstContainerApp.dll"]