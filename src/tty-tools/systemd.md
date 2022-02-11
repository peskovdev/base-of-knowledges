# Systemd

How to create unit from python with venv:

- Create `/lib/systemd/system/krolya.service`
- Write:
  ```
  [Unit]
  Description=Krolya - Telegram bot
  After=network.target

  [Service]
  Type=idle
  Restart=on-failure
  User=root
  ExecStart=/bin/bash -c 'cd /home/inauris/projects/freedom-pride-chat/crypto-kroleg && source ./venv/bin/activate && python bot.py'
  ExecReload=/usr/bin/node index.js

  [Install]
  WantedBy=multi-user.target
  ```
- `sudo systemctl daemon-reload`
- `sudo systemctl [status, start, stop, enable, disable] name`
