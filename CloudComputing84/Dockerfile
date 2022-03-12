#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CloudComputing84/CloudComputing84.csproj", "CloudComputing84/"]
RUN dotnet restore "CloudComputing84/CloudComputing84.csproj"
COPY . .
WORKDIR "/src/CloudComputing84"
RUN dotnet build "CloudComputing84.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CloudComputing84.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CloudComputing84.dll"]