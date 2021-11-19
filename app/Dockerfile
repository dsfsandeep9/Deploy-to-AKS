# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/sdk:6.0 as build-env
WORKDIR /app
EXPOSE 80

# Copy csproj and restore as distinct layers
COPY SampleWebApp/*.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
WORKDIR /app
RUN dotnet publish "SampleWebApp.csproj" -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:3.1
WORKDIR /WebApp
COPY --from=build-env /app/out ./
ENTRYPOINT ["dotnet", "SampleWebApp.dll"]
