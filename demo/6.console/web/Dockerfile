FROM microsoft/dotnet:2.0-sdk AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.0-runtime
ENV ASPNETCORE_URLS http://+:80
EXPOSE 5000
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "web.dll"]