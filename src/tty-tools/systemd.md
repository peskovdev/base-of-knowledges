# Systemd

#### How to create unit from python with venv:

- Create `/etc/systemd/system/krolya.service`
- Content:
```
[Unit]
Description=Krolya - Telegram bot
After=network.target

[Service]
User=inauris
Type=idle
Restart=always
ExecStart=/bin/bash -c 'cd /home/inauris/projects/krolya && source ./venv/bin/activate && python krolya.py'

[Install]
WantedBy=multi-user.target
```

---
#### How to autorun script as unit:
- Create `/etc/systemd/system/auto-git-pull.service`
- Content:
```
# auto-git-pull
[Unit]
Description=Automaticly pulling git-repositories
After=network.target

[Service]
User=inauris
Type=simple
ExecStart=/bin/bash '/home/inauris/.local/bin/auto-git-pull'

[Install]
WantedBy=multi-user.target
```
---
- `sudo systemctl daemon-reload`
- `sudo systemctl enable --now name`
