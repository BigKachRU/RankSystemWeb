FROM mcr.microsoft.com/dotnet/sdk:7.0 as build
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y libpng-dev libjpeg-dev curl libxi6 build-essential libgl1-mesa-glx
RUN curl -sL https://deb.nodesource.com/setup_lts.x | bash -
RUN apt-get install -y nodejs
WORKDIR /app
COPY . ./
RUN dotnet restore
RUN dotnet publish -c Release -o build
FROM mcr.microsoft.com/dotnet/aspnet:7.0 as runtime
WORKDIR /app
COPY --from=build /app/build .
ENTRYPOINT ["dotnet", "RankSystemWeb.dll"]
EXPOSE 80