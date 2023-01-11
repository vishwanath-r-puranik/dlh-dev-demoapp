# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /usr/app

# Copy project and restore as distinct layers
COPY . .
RUN dotnet restore 

RUN dotnet build  -c Release -o /usr/app/Build
RUN dotnet publish  -c Release -o /usr/app/Publish

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /usr/app
#Exposed 80 ports
EXPOSE 7192
ENV ASPNETCORE_URLS=http://+:7192
COPY --from=build /usr/app/Publish .
ENTRYPOINT ["dotnet", "AspNetCoreWebApi6.dll"]
