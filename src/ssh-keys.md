# SSH-Аuthentication
### Содержание:
  - [Генерация ключа](#keygen)
  - [Создание конфига](#config)
  - [Настройки конфига](#settings)
  - [Дополнительные ссылки](#links)
---

#### <a name='keygen'></a> Генерация ключа
Лучший алгоритм для генерации ключа (сложнее всего забрутфорсить):
```
ssh-keygen -t ed25519
```
Даем файлу нужное имя. Имя должно содержать путь.
Относительный путь строится от директории вызова функции.

Ключи должны оказаться здесь: `~/.ssh/key` and `~/.ssh/key.pub`

---

#### <a name='config'></a> Конфиг:

Создаем `~/.ssh/config`
```
Host example
  HostName hosts.domen.com
  IdentityFile /path/to/keyfile
  IdentitiesOnly yes

Host gitlab.com
  HostName gitlab.com
  IdentityFile ~/.ssh/gitlab-key
  IdentitiesOnly yes

Host github.com
  HostName github.com
  IdentityFile ~/.ssh/github-key
  IdentitiesOnly yes
``` 
<a name='settings'></a>
Важно дать корректное название хосту ведь когда мы добавляем
удаленный доступ к гит-репозиторию, мы выполняем:

```git remote add origin git@example:user/repository.git```

Где `example` это значение `HOST example` из конфига.<br>
Eсли вместо `HOST gitlab.com` указать `HOST glab`, то и при добавлении удаленного
доступа нужно будет писать:

```git remote add origin git@glab:user/repository```

С одной стороны это короче и удобней, а с другой нет, 
ведь сервисы при создании репа уже предлагают
команду для удаленного доступа со своим доменным именем.

---
#### <a name='links'></a> Дополнительные ссылки:
  - [Аутентификация на сервере с ssh](https://www.youtube.com/watch?v=IVHv3eVQa14)
