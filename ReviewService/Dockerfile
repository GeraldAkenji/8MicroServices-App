FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 5174

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["ReviewService.csproj", "./"]
RUN dotnet restore "ReviewService.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "ReviewService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ReviewService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ReviewService.dll"] 