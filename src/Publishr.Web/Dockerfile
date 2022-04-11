FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Publishr.Web/Publishr.Web.csproj", "Publishr.Web/"]
RUN dotnet restore "Publishr.Web/Publishr.Web.csproj"
COPY . .
WORKDIR "/src/Publishr.Web"
RUN dotnet build "Publishr.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Publishr.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Publishr.Web.dll"]
