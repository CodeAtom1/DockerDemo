#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
ENV ASPNETCORE_ENVIRONMENT=Development 
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DemoCoreApiWithDocker/DemoCoreApiWithDocker.csproj", "DemoCoreApiWithDocker/"]
RUN dotnet restore "DemoCoreApiWithDocker/DemoCoreApiWithDocker.csproj"
COPY . .
WORKDIR "/src/DemoCoreApiWithDocker"
RUN dotnet build "DemoCoreApiWithDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DemoCoreApiWithDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DemoCoreApiWithDocker.dll"]