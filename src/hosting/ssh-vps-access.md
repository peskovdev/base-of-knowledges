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


# links:
```
First init:
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04

Nginx:
https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04

SSL:
https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04

Deploy files:
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-react-application-with-nginx-on-ubuntu-20-04
```
Whole commands:

```
useadd...
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install -y vim mosh tmux htop git curl wget unzip zip gcc build-essential make

# packages
sudo apt-get install -y zsh tree redis-server nginx zlib1g-dev libbz2-dev libreadline-dev llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev liblzma-dev python3-dev python-imaging python3-lxml libxslt-dev python-libxml2 python-libxslt1 libffi-dev libssl-dev python-dev gnumeric libsqlite3-dev libpq-dev libxml2-dev libxslt1-dev libjpeg-dev libfreetype6-dev libcurl4-openssl-dev supervisor
# oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# plugins
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
git clone https://github.com/jeffreytse/zsh-vi-mode $ZSH_CUSTOM/plugins/zsh-vi-mode
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
