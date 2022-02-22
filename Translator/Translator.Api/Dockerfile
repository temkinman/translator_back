#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Translator.Api/Translator.Api.csproj", "Translator.Api/"]
RUN dotnet restore "Translator.Api/Translator.Api.csproj"
COPY . .
WORKDIR "/src/Translator.Api"
RUN dotnet build "Translator.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Translator.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Translator.Api.dll"]