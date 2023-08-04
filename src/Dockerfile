# syntax=docker/dockerfile:1

# Set the build context to the parent directory containing the "src" directory
WORKDIR /app

# Copy the entire project into the build context (including "src" directory)
COPY . .

# Rest of your Dockerfile
FROM mcr.microsoft.com/dotnet/sdk:7.0 as build-env
WORKDIR /app/src
RUN dotnet restore
RUN dotnet publish -c Release -o /publish

FROM mcr.microsoft.com/dotnet/aspnet:6.0 as runtime
WORKDIR /publish
COPY --from=build-env /publish .
EXPOSE 8080
ENTRYPOINT ["dotnet", "myWebApp.dll"]
