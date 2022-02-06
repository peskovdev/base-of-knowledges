# Git - Шпаргалка
### Содержание:
  - [Настройка конфига](#config)
  - [Работа с ветками](#branch)
    - [Создание новой ветки](#creating-branch)
    - [Стянуть ветку из удаленного репа](#fetch-branch)
    - [Удалить ветку](#delete-branch)
    - [Переключить ветку](#switch-branch)
  - [](#)
  - [](#)
---

## <a name='config'></a> Конфиг:
```
git config --global user.name 'inauris'
git config --global user.email 'inauris@protonmail.com'
git config --global core.editor 'nvim'
```

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

#### <a name='switch-branch'></a> Переключение ветки:
```
git checkout name
git switch name
```

#### <a name=''></a> 
