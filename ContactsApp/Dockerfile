# Use the official .NET Core SDK image as a build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy the solution file and restore dependencies =1 
COPY --chown=user:user *.sln .
RUN ls -la
RUN dotnet restore

# Copy the remaining source code and build the application
COPY . .
WORKDIR /app/ContactsApp
RUN dotnet build -c Release -o /app/build

# Run tests if any

# Publish the application
FROM build AS publish
RUN dotnet publish -c Release -o /app/publish

# Final stage: create the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=publish /app/publish .

# Set the entry point for the application
ENTRYPOINT ["dotnet", "ContactsApp.dll"]