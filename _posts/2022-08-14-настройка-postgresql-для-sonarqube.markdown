---
layout: post
title:  "Настройка postgresql для sonarqube"
date:   2022-08-14 11:04:00 +0300
categories: sonarqube
---
Для подключения postgresql 10 к sonarqube необходимо выполнить следующие действия:

1. Создать пользователя (пример для `pgAdmin 4 (v. 6.8)`):
  - Вызвать контекстное меню у пункта `Login/Group Roles` и выбрать пункт `Create > Login/Group Role...`.
  - На вкладке `General` ввести имя пользователя (например, `sonar`).
  - На вкладке `Defenition` указать пароль (например, `sonar`).
  - На вкладке `Privileges` установить включатель `Can login?` и `Create databases?`.

2. Создать новую базу данных и дать пользователю `sonar` полные права на неё:
  - Вызвать контекстное меню у пункта `Databases` и выбрать пункт `Create > Database...`.
  - На вкладке `General` ввести имя базы (например, `sonarqube`) и указать владельца.
  - На вкладке `Security` в списке `Privileges` необходимо дать все права пользователю `sonar` на создаваемую таблицу.

3. Внести правки в конфигурационный файл `conf\sonar.properties`

```properties
# User credentials.
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar

#----- PostgreSQL 9.3 or greater
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
```

### Дополнительные ссылки

[Краткая инструкиция на github][sonarqube-config].


[sonarqube-config]: https://gist.github.com/marek-panek/8b5fec0ad623926b110267e0b7d66559
