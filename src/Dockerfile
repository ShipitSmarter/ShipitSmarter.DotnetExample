FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /App

# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
# https://mcr.microsoft.com/v2/dotnet/aspnet/tags/list
#FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine
FROM mcr.microsoft.com/dotnet/aspnet:7.0.1-alpine3.16
#FROM mcr.microsoft.com/dotnet/aspnet:6.0.10-alpine3.16  
WORKDIR /App
COPY --from=build-env /App/out .
ENTRYPOINT ["dotnet", "DotnetExample.dll"]
