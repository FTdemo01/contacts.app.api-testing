# Use the .NET SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env

# Set the working directory to where your project file exists
WORKDIR /App

# Copy the project files
COPY *.sln ./

# Restore dependencies
RUN dotnet restore

# Build and publish the application
RUN dotnet publish -c Release -o out

# Build the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

# Set the working directory for the runtime image
WORKDIR /App

# Copy the published output from the build stage
COPY --from=build-env /App/out .

# Command to run when the container starts
ENTRYPOINT ["dotnet", "ContactsApp.dll"]