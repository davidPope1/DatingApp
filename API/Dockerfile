# Use the official .NET Core SDK as a parent image
FROM mcr.microsoft.com/dotnet/sdk:8.0.300 AS build

# Set the current working directory
WORKDIR /app

# Copy the project file and restore any dependencies (use .csproj for the project name)
COPY *.csproj ./

RUN dotnet restore

# Copy the rest of the application code
COPY . .

# Publish the application
RUN dotnet publish -c Release -o /publish

# Build the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0.5 AS runtime

WORKDIR /app

COPY --from=build /publish .

# Expose the port your application will run on
EXPOSE 5000

# Start the application
ENTRYPOINT [ "dotnet", "API.dll" ]