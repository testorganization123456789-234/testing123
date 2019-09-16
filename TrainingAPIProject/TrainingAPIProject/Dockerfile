FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["TrainingAPIProject/TrainingAPIProject.csproj", "TrainingAPIProject/"]
RUN dotnet restore "TrainingAPIProject/TrainingAPIProject.csproj"
COPY . .
WORKDIR "/src/TrainingAPIProject"
RUN dotnet build "TrainingAPIProject.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TrainingAPIProject.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TrainingAPIProject.dll"]