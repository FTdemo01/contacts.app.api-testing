# Use the official .NET Core SDK image as a build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /var/lib/jenkins/workspace/demo2_main-docker/contacts.app.api-testing/ContactsApp

# Copy the solution file and restore dependencies =1 
# COPY --chown=user:user *.sln .

COPY . ./
RUN ls -la
RUN dotnet restore

# Copy the remaining source code and build the application
# COPY . .
# WORKDIR /var/lib/jenkins/workspace/demo2_main-docker/contacts.app.api-testing/ContactsApp/ContactsApp
# RUN dotnet build -c Release -o /var/lib/jenkins/workspace/demo2_main-docker/contacts.app.api-testing/ContactsApp/build

# Run tests if any

# Publish the application
# FROM build AS publish
RUN dotnet publish -c Release -o out

# Final stage: create the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /var/lib/jenkins/workspace/demo2_main-docker/contacts.app.api-testing/ContactsApp
COPY --from=build /var/lib/jenkins/workspace/demo2_main-docker/contacts.app.api-testing/ContactsApp/out .

# Set the entry point for the application
ENTRYPOINT ["dotnet", "ContactsApp.dll"]
