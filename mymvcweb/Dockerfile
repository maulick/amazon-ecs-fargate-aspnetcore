# Use the official .NET SDK image
FROM mcr.microsoft.com/dotnet/sdk:3.0 AS build-env

WORKDIR /app

# Copy csproj and restore as distinct layers
COPY mymvcweb/*.csproj ./mymvcweb/
RUN dotnet restore mymvcweb/mymvcweb.csproj

# Copy everything else
COPY . ./

# Clean before publishing to avoid duplicate files
RUN dotnet clean mymvcweb/mymvcweb.csproj && \
    dotnet publish mymvcweb/mymvcweb.csproj -c Release -o out

# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:3.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "mymvcweb.dll"]

