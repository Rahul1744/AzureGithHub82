#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["azure82/azure82.csproj", "azure82/"]
RUN dotnet restore "azure82/azure82.csproj"
COPY . .
WORKDIR "/src/azure82"
RUN dotnet build "azure82.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "azure82.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "azure82.dll"]