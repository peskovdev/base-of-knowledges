# Docker - Шпаргалка
### Содержание:
  - [Установка](#install)
  - [Вызов доки](#docs)
  - [Узнать инфу](#docs)
      - В целом про контейнеры в системе
      - Про все образы
  - [Запустить/остановить контейнер](#launch)
  - [Удалить все остановленные контейнеры/образы](#deleteexited)
  - [Образы](#images)
  - [Запуск контейнеров](#run)
  - [Dockerfile](#dockerfile)
  - [Build](#build)
  - [docker-compose](#dockercompose)
---

## <a name='install'></a> Установка:
```
yay -S docker docker-compose
sudo systemctl enable --now docker.service

# for remove sudo do following && relogin or restart docker.service
sudo gpasswd -a user docker
(on ubuntu sudo usermod -aG docker user)
```

## <a name='docs'></a> Вызов доки:
- `docker` - общая инфа
- `docker command --help` - подробная инфа по конкретной команде

## <a name='docs'></a> Узнать инфу:
- В целом про контейнеры в системе: `docker info`
- Про все образы в системе: `docker images`
- Про все контейнеры в системе: `docker ps -a`

## <a name='launch'></a> Запустить/Остановить контейнер:
```
docker run ...
docker rename container_name new_name

docker start container_name
docker stop container_name
docker restart container_name

# пауза - заставить подвиснуть
docker pause container_name
docker unpause container_name
```

Узнать инфу о контейнере:

```docker inspect container_name```
## <a name='deleteexited'></a> Удалить все остановленные контейнеры/образы:
```
docker rm -v $(docker ps -aq -f status=exited)
docker rmi $(docker images -q) --force
```

## <a name='images'></a> Образы:
Скачать образ:
```
docker pull image:<version>
```
Загрузить образ:
```
docker build -t image_name ./docker_dir/
docker push user/image_name
```

## <a name='run'></a> Запуск контейнеров:

##### `run`
Скачивает образ и запускает контейнер
- `docker run`:
  - `-d, --detach` - run ib background & print container ID
  - `-p, --publish list` - connect ports
  - `-it` - запуск в интерактивном режиме
  - `--name container_name` - задать имя контейнера

## <a name='dockerfile'></a> Dockerfile:

```
# In comment "equal to" console command

# docker run -it ubuntu bash
FROM ubuntu

# from - to
COPY . /java

# pwd
WORKDIR /java

EXPOSE 8001

# Execute only on build
RUN javac Main.java

# Execute on every start
CMD [ "java", "Main" ]

```
## <a name='build'></a> Build:

```
docker build -t name_of_image ./dir
```


## <a name='dockercompose'></a> docker-compose:
yaml-structure:
```
services:
  django:
    build: ./
    restart: on-failure
    container_name: django
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - ./.django-volume/:/usr/src/app
    ports:
      - "8000:8000"
    depends_on:
      - pgdb

  pgdb:
    image: postgres
    restart: always
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=test123
    container_name: pgdb
    volumes:
      - pgdbdata:/var/lib/postgresql/data

volumes:
  pgdbdata: null
```
Команды:
- `docker-compose up -d(detach) --build` 
- `docker-compose build`
- `docker-compose run service_name command`
