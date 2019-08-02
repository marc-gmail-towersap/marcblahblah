FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["marccoreweb/marccoreweb.csproj", "marccoreweb/"]
RUN dotnet restore "marccoreweb/marccoreweb.csproj"
COPY . .
WORKDIR "/src/marccoreweb"
RUN dotnet build "marccoreweb.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "marccoreweb.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "marccoreweb.dll"]