# 1. Этап сборки
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# 2. Копируем файлы проекта и восстанавливаем зависимости
COPY ["UserManagementApp.csproj", "."]
RUN dotnet restore "UserManagementApp.csproj"

COPY . .
RUN dotnet publish -c Release -o /app

# 3. Этап запуска
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app

# 4. Копируем собранное приложение
COPY --from=build /app .

# 5. Указываем порт (Render использует $PORT)
ENV ASPNETCORE_URLS=http://*:$PORT

# 6. Точка входа
ENTRYPOINT ["dotnet", "UserManagementApp.dll"]