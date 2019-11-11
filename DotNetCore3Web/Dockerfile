FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["DotNetCore3Web/DotNetCore3Web.csproj", "DotNetCore3Web/"]
RUN dotnet restore "DotNetCore3Web/DotNetCore3Web.csproj"
COPY . .
WORKDIR "/src/DotNetCore3Web"
RUN dotnet build "DotNetCore3Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DotNetCore3Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DotNetCore3Web.dll"]