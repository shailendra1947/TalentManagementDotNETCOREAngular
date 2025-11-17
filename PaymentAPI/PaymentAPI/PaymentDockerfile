# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore
COPY ["PaymentAPI/PaymentAPI.csproj", "PaymentAPI/"]
RUN dotnet restore "PaymentAPI/PaymentAPI.csproj"

# Copy everything and publish
COPY . .
WORKDIR /src/PaymentAPI
RUN dotnet publish "PaymentAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:80
EXPOSE 80
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "PaymentAPI.dll"]