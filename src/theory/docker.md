# Docker

Контейнерезация. Все процессы работают на физическом хост-сервере.
Бенефиты:
- Переиспользуемсоть
- Тестирумость


### Docker-workflow
Образы используются для создания контейнера. Образы расположены в реестрах (публичные и приватные).

главный паблик реестр "Docker-hub": https://hub.docker.com

Контейнеры - содержит все что необходимо для работы приложения.
Этакий финальный продукт. Собранная солянка образов, зависимостей, файлов проекта.

Контейнеры могут быть созданы, запущены, установлены, перенесены, удалены итд.


## Docker-compose

yaml-structure:
```
services:
  mysql:
    image: mariadb
    restart: always
    volumes:
      - ./databases:/var/lib/mysql
      - ./real/path:/path/in/container
    environment:
      - MYSQL_ROOT_PASSWORD=password
    ports:
      - "3307:3306" # machine_port:container_port
  mailserver:
    image: 'dkadevelop/mailserver:latest'
    restart: always
    volumes:
      - ./databases:/var/lib/mysql
      - ./real/path:/path/in/container
      - ./real/path:/path/in/container
      - ./real/path:/path/in/container
    ports:
      - "110:110" # machine_port:container_port
      - "25:25"
      - "8087:80"
    command: /usr/bin/supervisord
    tty: true
    stdin_open: true
```

Команды:
- `docker-compose up`
