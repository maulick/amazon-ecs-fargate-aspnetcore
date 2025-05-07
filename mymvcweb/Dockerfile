# Use the official .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build-env

WORKDIR /app

# Copy csproj and restore as distinct layers
COPY mymvcweb/mymvcweb.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet clean  # Clean up any previous build artifacts
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.0

WORKDIR /app

# Copy the published app from the build environment
COPY --from=build-env /app/out .

# Set the entry point for the application
ENTRYPOINT ["dotnet", "mymvcweb.dll"]

# Set the environment variable to specify the URL the app listens on
ENV ASPNETCORE_URLS=http://+:5000

# Expose port 5000
EXPOSE 5000

