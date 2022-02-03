# GitLab and GitHub pages
Содержание:
  - [Настройка на гитлабе](#gitlab)
    - [Структура директории](#structure)
    - [book.toml](#mdbook)
    - [gitlab-ci.yml](#yml)
    - [gitlab-runner](#runners)

## <a name='gilab'></a> Создание сайта на гитлаб:

##### В репозитории отображаем следущую структуру:
  - src/
  - book.toml:
  - gitlab-ci.yml

В директории `src/` лежат все .md раскиданные по дочерним директориям

##### <a name='mdbook'></a> Заполняем book.toml следующим образом
```
[book]
authors = ['inauris']
language = 'ru'
multilingual = false
src = 'src'
title = 'GitLab Pages mdbook'

[build]
build-dir = 'public'
# create-missing = false

[preprocessor.toc]
command = './mdbook-toc'
renderer = ['html']
```
##### <a name='yml'></a> Заполняем .yml конфиг
```
pages:
  stage: deploy
  script:
  - wget https://github.com/badboy/mdbook-toc/releases/download/0.2.4/mdbook-toc-0.2.4-x86_64-unknown-linux-gnu.tar.gz
  - wget https://github.com/rust-lang/mdBook/releases/download/v0.3.7/mdbook-v0.3.7-x86_64-unknown-linux-gnu.tar.gz
  - tar xvzf mdbook-v0.3.7-x86_64-unknown-linux-gnu.tar.gz
  - tar xvzf mdbook-toc-0.2.4-x86_64-unknown-linux-gnu.tar.gz
  - ./mdbook build
  artifacts:
    paths:
    - public
  only:
  - master
```
  
##### <a name='runners'></a> Own gitlab-runner
Для работы пайпалайнов необходимы раннеры. Есть раннеры предоставляемые самим
гитлабом, но для их использования аккаунт необходимо подтвердить картой.

Есть 2 вариант без подтверждения, а именно, установить свои кастомные раннеры:
  ```
  # Download the binary for your system
  sudo curl -L --output /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64

  # Give it permission to execute
  sudo chmod +x /usr/local/bin/gitlab-runner

  # Create a GitLab Runner user
  sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

  # Install and run as a service
  sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
  sudo gitlab-runner start

  ```



## <a name='github'></a> Создание сайта на гитхаб:
- Создаем Репозиторий
- Заходим в репозиторий в settings
- В левом меню выбираем pages
- В Source выбираем ветку и директорию корня проекта
- Сохраняем.
- ( Ставим кастомный url если хочеца )
