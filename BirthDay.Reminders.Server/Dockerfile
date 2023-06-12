FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["BirthDay.Reminders.Server/BirthDay.Reminders.Server.csproj", "BirthDay.Reminders.Server/"]
RUN dotnet restore "BirthDay.Reminders.Server/BirthDay.Reminders.Server.csproj"
COPY . .
WORKDIR "/src/BirthDay.Reminders.Server"
RUN dotnet build "BirthDay.Reminders.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BirthDay.Reminders.Server.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BirthDay.Reminders.Server.dll"]
