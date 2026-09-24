# -LO02_-_Linux

## Цель работы
Написать bash-скрипт, принимающий город, выводящий температуру и влажность; настроить nginx; 
запускать скрипт по cron раз в минуту с записью результата в index.html

## 1. Установка ПО

sudo apt update

sudo apt install nginx jq curl -y

## 2. Создание index.html
sudo touch /var/www/html/index.html

sudo chmod a+w /var/www/html/index.html

ls -l /var/www/html/
<img width="682" height="111" alt="image" src="https://github.com/user-attachments/assets/d2c74d92-a532-4540-a132-25bffb07f25d" />


## 3. Проверка API погоды
curl -s --max-time 60 "wttr.in/Perm?format=j1" -o /tmp/weather.json

jq -r '.["current_condition"][0] | .temp_C, .humidity' /tmp/weather.json
<img width="803" height="71" alt="image" src="https://github.com/user-attachments/assets/0d4b9c37-92c0-423d-b871-717c3046e3e6" />


## 4. Скрипт ~/weather.sh
nano ~/weather.sh

chmod +x ~/weather.sh

~/weather.sh Perm
<img width="955" height="229" alt="image" src="https://github.com/user-attachments/assets/d7415a5e-ade2-4735-9a9b-5a79887977fb" />


## 5. Настройка и проверка cron
crontab -e

добавлено: * * * * * /home/alyon/weather.sh Perm > /dev/null 2>&1

service cron status
<img width="1043" height="494" alt="image" src="https://github.com/user-attachments/assets/c47aaae5-b39c-4a51-b139-6b94780ef161" />

## 6. Доказательство работы cron

Через 1–2 минуты после настройки cron:

curl 127.0.0.1

<img width="1087" height="158" alt="image" src="https://github.com/user-attachments/assets/623940bc-039f-42a0-8bcc-97a3dfffc3b2" />
# Вывод
Освоены: bash-скрипты (аргументы, here-doc), парсинг JSON через jq, настройка nginx и прав доступа, планировщик cron в WSL. Все требования задания выполнены.
