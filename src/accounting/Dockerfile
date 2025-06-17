FROM  mcr.microsoft.com/dotnet/sdk:8.0 AS build
# Use the official Python image as a base
WORKDIR /src
# Copy the project files to the container   
COPY ["src/accounting/Accounting.csproj", "src/accounting/"]
# Restore the project dependencies  
RUN dotnet restore "src/accounting/Accounting.csproj"
# Copy the rest of the application code
COPY src/accounting/ .
# Build the application
RUN dotnet build "src/accounting/Accounting.csproj" -c Release -o /app/build    
# Publish the application
RUN dotnet publish "src/accounting/Accounting.csproj" -c Release -o /app/publish /p:UseAppHost=false
# Use the official ASP.NET runtime image as a base for the final image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final   
# Set the working directory in the final image
WORKDIR /app
# Copy the published application from the build stage
COPY --from=build /app/publish .
# Expose the port the app runs on
EXPOSE 8080
# Set the entry point for the application
ENTRYPOINT ["dotnet", "Accounting.dll"]
