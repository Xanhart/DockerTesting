#FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
#WORKDIR /src
#COPY *.sln ./
#COPY hello-mvc2.0/hello-mvc2.0.csproj hello-mvc2.0/
#RUN dotnet restore
#COPY . .
#WORKDIR /src/hello-mvc2.0
#RUN dotnet build -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "hello-mvc2.0.dll"]
#

#FROM microsoft/aspnetcore:1.1
#ARG source
#WORKDIR /app
#EXPOSE 80
#COPY ${source:-obj/Docker/publish} .
#ENTRYPOINT ["dotnet", "hello-mvc.dll"]

FROM microsoft/aspnetcore-build:2.0 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "hello-mvc2.0.dll"]