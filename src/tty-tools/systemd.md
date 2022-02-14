# Systemd

How to create unit from python with venv:

- Create `/etc/systemd/system/krolya.service` and `/etc/systemd/system/auto-git-pull.service`
- Content:
  ```
  # krolya
  [Unit]
  Description=Krolya - Telegram bot
  After=network.target

  [Service]
  User=inauris
  Type=idle
  Restart=on-failure
  ExecStart=/bin/bash -c 'cd /home/inauris/projects/krolya && source ./venv/bin/activate && python krolya.py'

  [Install]
  WantedBy=multi-user.target


  # auto-git-pull
  [Unit]
  Description=Automaticly pulling git-repositories
  After=network.target

  [Service]
  Type=simple
  User=inauris
  ExecStart=/bin/bash '/home/inauris/.local/bin/auto-git-pull'

  [Install]
  WantedBy=multi-user.target
  ```

- `sudo systemctl daemon-reload`
- `systemctl --user [start, stop, enable, disable] name`
