FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY "eTickets.csproj" .
RUN dotnet restore "eTickets.csproj"
COPY . .
RUN dotnet build . -c Release -o /app/build

# RUN apt-get install curl

FROM build AS publish
RUN dotnet publish "eTickets.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "eTickets.dll"]