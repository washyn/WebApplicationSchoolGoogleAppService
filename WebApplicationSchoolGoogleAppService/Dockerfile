#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["WebApplicationSchoolGoogleAppService/WebApplicationSchoolGoogleAppService.csproj", "WebApplicationSchoolGoogleAppService/"]
RUN dotnet restore "WebApplicationSchoolGoogleAppService/WebApplicationSchoolGoogleAppService.csproj"
COPY . .
WORKDIR "/src/WebApplicationSchoolGoogleAppService"
RUN dotnet build "WebApplicationSchoolGoogleAppService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplicationSchoolGoogleAppService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplicationSchoolGoogleAppService.dll"]


# FROM mcr.microsoft.com/dotnet/aspnet:5.0-alpine

# WORKDIR /app
# COPY . .

# ENTRYPOINT ["dotnet", "WebApplicationSchoolGoogleAppService.dll"]



# FROM mcr.microsoft.com/dotnet/aspnet:5.0-alpine
# ADD ./ /app
# #ENV ASPNETCORE_URLS=https://*:${PORT}
# WORKDIR /app
# ENTRYPOINT [ "dotnet", "WebApplicationSchoolGoogleAppService.dll" ]