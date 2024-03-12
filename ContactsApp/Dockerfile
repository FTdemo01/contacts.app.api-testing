# Use the .NET SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /App

# Copy csproj and restore as distinct layers
COPY *.sln ./
RUN dotnet restore ContactsApp.sln

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /App
COPY --from=build-env /App/out .
ENTRYPOINT ["dotnet", "YourAppName.dll"]
