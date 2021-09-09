#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["aws-proton-demo-app/aws-proton-demo-app.csproj", "aws-proton-demo-app/"]
RUN dotnet restore "aws-proton-demo-app/aws-proton-demo-app.csproj"
COPY . .
WORKDIR "/src/aws-proton-demo-app"
RUN dotnet build "aws-proton-demo-app.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aws-proton-demo-app.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aws-proton-demo-app.dll"]