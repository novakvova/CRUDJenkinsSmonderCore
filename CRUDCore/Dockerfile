FROM microsoft/dotnet:2.2-sdk-alpine AS builder #З докер хаба качаємо образ із докер хаба, якщо alpine менше жере місця
WORKDIR /source  #робоча папка докера
EXPOSE 80 #Рубаємо на 80 порті в середині докера
#EXPOSE 5001

#RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
#RUN apt-get install -y nodejs
RUN apk --no-cache add nodejs nodejs-npm #Ставмо в лінокс nodejs nodejs-npm

COPY *.csproj . # Копіруємо в середину докера файл з роширенням .csproj
RUN dotnet restore # Підкачуємо пакети для роботи проекта dotnet

COPY ./ ./ # Копіємо усі остальні папки і файли в докер

RUN dotnet publish "./CRUDCore.csproj" --output "./dist" --configuration Release --no-restore # Робимо publish так як звичайно
FROM microsoft/dotnet:2.2-aspnetcore-runtime-alpine # Щоб запустити поптрібно для рана

WORKDIR /app #Створили робочу паку
COPY --from=builder /source/dist . # Туди скопіювати, те що на білдили

#EXPOSE 80
ENTRYPOINT ["dotnet", "CRUDCore.dll"] # Запускаємо наш сайт на кестрелі