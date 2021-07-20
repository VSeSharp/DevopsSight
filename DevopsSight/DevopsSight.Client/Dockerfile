#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DevopsSight.Client.csproj", "DevopsSight.Client/"]
#COPY ["DevopsSight.Client/DevopsSight.Client.csproj", "DevopsSight.Client/"]
RUN dotnet restore "DevopsSight.Client/DevopsSight.Client.csproj"
COPY . .
WORKDIR "/src/DevopsSight.Client"
RUN dotnet build "DevopsSight.Client.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevopsSight.Client.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevopsSight.Client.dll"]