# Git - Шпаргалка
### Содержание:
  - [Настройка конфига](#config)
  - [Remote](#remote)
    - [Смена url](#set-url)
  - [Работа с ветками](#branch)
    - [Создание новой ветки](#creating-branch)
    - [Стянуть ветку из удаленного репа](#fetch-branch)
    - [Удалить ветку](#delete-branch)
    - [Удалить ветку в удаленном репозитории](#delete-remote-branch)
    - [Переключить ветку](#switch-branch)
  - [Коммиты](#commits)
    - [Отменить коммит](#cancelCommit)
    - [Изменить сообщение коммита](#renameCommit)
    - [Коммит без 'add'](#commits!add)
    - [Удалить только в index](#rmCache)
  - [Удаление файлов](#deleting)
    - [git rm](#deleteWithGit)
  - [Переименование файлов](#renaming)
  - [Игнор изменений файлов остающихся в репе](#ignore-exist)
---

## <a name='config'></a> Конфиг:
```
git config --global user.name 'inauris'
git config --global user.email 'inauris@protonmail.com'
git config --global core.editor 'nvim'
git config --global core.excludesFile ~/.gitignore
```

## <a name='remote'></a> Remote:
#### <a name='set-url'></a> Смена url:
```
git remote set-url origin git@gitlab.com:freedom-pride-chat/pheidippides.git
```
---
## <a name='branch'></a> Работа с ветками:
#### <a name='creating-branch'></a> Создание ветки:
```
git branch name

# Создание + переключение одновременно:
git switch -c name
git checkout -b name
```

#### <a name='fetch-branch'></a> Стянуть ветку с удаленного репа:
 
```
git checkout -b name origin/name
git switch -c name origin/name
```

#### <a name='delete-branch'></a> Удаление ветки:
```
git branch -D name
```
#### <a name='delete-remote-branch'></a> Удаление ветки удаленного репозитория:
```
gp origin --delete origin/name
```

#### <a name='switch-branch'></a> Переключение ветки:
```
git checkout name
git switch name
```
---

## <a name='commits'></a> Коммиты:

#### <a name='cancelCommit'></a> Отменить коммит
```
# Оставить изменения
git reset --soft HEAD~

# Удалить изменения
git reset --hard HEAD~
```
#### <a name='renameCommit'></a> Изменить сообщение коммита
```
git commit --amend

# если хотите запушить изменение на удаленный репозиторий:
gp -f

# если ввели локально, но потом передумали:
git pull --rebase
```
#### <a name='commits!add'></a> Коммит без 'add'
```
git commit -a
git commit path/to/file.type

alias.commitall '!git add .[-A]; git commit'
```

#### <a name='rmCache'></a> Удалить только в index
```
git rm -r --cached name
```
---

## <a name='deleting'></a> Удаление:
Для удаления файла достаточно удалить файлы и добавить изменения в индекс.
Дальше сможем закомитить (Чтоб изменения прошли - ветка должна быть с ребейзом)

#### <a name='deleteWithGit'></a> Гитовское удаление:
Удаляет не только из воркспейса, но и из индекса
```
git rm path/to/name

flags:
  -r # for directory
  -f #forse
  -- cached # only index
```

#### <a name='renaming'></a> Переименование:
Можно просто переименовать и проиндексировать старый 'удаленный' и 'новый' файл
При попадании в индекс гит по-контрольной сумме определит что это переименование.
Для того чтоб переименование произошло сразу можно использовать команду:
```
git mv hello.html index.html
```
#### <a name='ignore-exist'></a> Игнор изменений файлов остающихся в репе:
Файл будет оставаться в репозитории, но гит будет игнорить изменения:
```
git update-index --assume-unchanged flameshot/.config/flameshot/flameshot.ini
```
