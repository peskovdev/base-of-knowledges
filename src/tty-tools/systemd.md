# Systemd

How to create unit from python with venv:

- Create `/lib/systemd/user/name.service`
- Content:
  ```
  [Unit]
  Description=Krolya - Telegram bot
  After=network.target
  
  [Service]
  Type=idle
  Restart=on-failure
  ExecStart=/bin/bash -c 'cd /home/inauris/projects/krolya && source ./venv/bin/activate && python krolya.py'
 
  [Install]
  WantedBy=multi-user.target
  
  or
  
  [Unit]
  Description=Auto git pull
  After=network.target
  
  [Service]
  Type=simple
  ExecStart=/bin/bash -c '/home/inauris/.local/bin/auto-git-pull'
  
  [Install]
  WantedBy=multi-user.target
  ```
- `sudo systemctl daemon-reload`
- `systemctl --user [start, stop, enable, disable] name`
