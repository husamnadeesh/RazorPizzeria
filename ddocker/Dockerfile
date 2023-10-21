FROM mcr.microsoft.com/dotnet/sdk:7.0-alpine AS build-env

WORKDIR /dotnet-example-app

COPY ["RazorPizzeria.csproj", "."]

# # Restore as distinct layers
RUN dotnet restore "RazorPizzeria.csproj"
COPY . .

# Build and publish a release
RUN dotnet build "RazorPizzeria.csproj" -c Release -o out
RUN dotnet publish "RazorPizzeria.csproj" -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0-alpine
WORKDIR /RazorPizzeria
COPY --from=build-env /RazorPizzeria/out .

EXPOSE 80

ENTRYPOINT ["dotnet", "RazorPizzeria.dll"]