FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app

ENV ASPNETCORE_URLS="http://+:80"
EXPOSE 80
 
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app
COPY . .
RUN dotnet restore
RUN dotnet build -c Release -o /app/build
 
FROM build AS publish
RUN dotnet publish -c Release -o /app/publish
 
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "backend.dll"]