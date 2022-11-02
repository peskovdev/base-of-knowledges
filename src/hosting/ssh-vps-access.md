# SSH-Аuthentication
### Содержание:
  - Добавление ключа
    - [Генерация ключа](#keygen)
    - [Добавление ключей на сервер](#adding)
    - [Создание конфига](#config)
  - Блокировка аутентификации по-паролю
---

#### <a name='keygen'></a> Генерация ключа
Лучший алгоритм для генерации ключа (сложнее всего забрутфорсить):
```
ssh-keygen -t ed25519
```
Даем файлу имя `vps-key`. Имя должно содержать путь.
Относительный путь строится от директории вызова функции.

Ключи должны оказаться здесь: `~/.ssh/vps-key` and `~/.ssh/vps-key.pub`

---
#### <a name='adding'></a> Добавление ключей на сервер:
```
cat ~/.ssh/vps-key.pub | ssh user@host 'cat >> .ssh/authorized_keys'
```

#### <a name='config'></a> Конфиг:

Добавляем в конфиг `~/.ssh/config` (необходимо если имена ключей кастомные):
```
# host = ip
Host host
  HostName host
  IdentityFile ~/.ssh/vps-key
  IdentitiesOnly yes
``` 
