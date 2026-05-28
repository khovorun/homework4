Завдання 1. Менеджери пакетів

bash
sudo apt update
sudo apt install tree -y
tree --version
dpkg -l | grep tree
sudo apt remove tree -y

Завдання 2. Керування сервісами

bash
systemctl status cron
sudo systemctl stop cron
systemctl status cron
sudo systemctl start cron
sudo systemctl enable cron


Завдання 3. Робота з логами
bash
cd /var/log
tail -10 syslog
journalctl -p err
journalctl -u cron


Завдання 4. Власний сервіс

Скрипт
bash
nano ~/myscript.sh
chmod +x ~/myscript.sh


Вміст:

bash
#!/bin/bash
while true
do
    date >> /home/huawei/date_log.txt
    sleep 1
done


Systemd service
bash
sudo nano /etc/systemd/system/myscript.service

Вміст:
ini
[Unit]
Description=My date logger service
After=network.target

[Service]
ExecStart=/home/huawei/myscript.sh
Restart=always
User=huawei

[Install]
WantedBy=multi-user.target

Команди:
bash
sudo systemctl daemon-reload
sudo systemctl start myscript
systemctl status myscript
tail /home/huawei/date_log.txt
sudo systemctl enable myscript
systemctl is-enabled myscript
