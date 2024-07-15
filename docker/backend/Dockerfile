# Stage 1: Build .NET App
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /source

# Copy the csproj and restore as distinct layers
COPY ./backend/*.sln ./
COPY ./backend/*.csproj ./backend/
RUN dotnet restore ./backend/*.csproj

# Copy the rest of the application and build
COPY ./backend/. ./backend/
WORKDIR /source/backend
RUN dotnet publish -c Release -o /app

# Stage 2: Run .NET App
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "backend.dll"]
EXPOSE 80
