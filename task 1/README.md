## Задача 1

Сценарий выполнения задачи:
- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
- Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: ```{"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}```
- Зарегистрируйтесь и создайте публичный репозиторий  с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
- скачайте образ nginx:1.29.0;
- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
```
- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).
- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

## Ответ

https://hub.docker.com/repository/docker/khurmatov94/custom-nginx/general

## Задача 2
1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080
2. Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```
4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

## Ответ

<img width="1533" height="589" alt="Задача 2" src="https://github.com/user-attachments/assets/6392f986-2e0b-43fa-a4df-9eab573d3ccf" />

## Задача 3
1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3. Выполните ```docker ps -a``` и объясните своими словами почему контейнер остановился.
4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8. Запомните(!) и выполните команду ```nginx -s reload```, а затем внутри контейнера ```curl http://127.0.0.1:80 ; curl http://127.0.0.1:81```.
9. Выйдите из контейнера, набрав в консоли  ```exit``` или Ctrl-D.
10. Проверьте вывод команд: ```ss -tlpn | grep 127.0.0.1:8080``` , ```docker port custom-nginx-t2```, ```curl http://127.0.0.1:8080```. Кратко объясните суть возникшей проблемы.
11. * Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. [пример источника](https://www.baeldung.com/linux/assign-port-docker-container)
12. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

## Ответ

п.1 - п.3
<img width="998" height="306" alt="Задача 3 1" src="https://github.com/user-attachments/assets/1b640379-f7f5-4781-97ed-68ebecdc0d64" />

Комбинация клавиш Ctrl-C передает контейнеру сигнал SIGINT, и контейнер останавливается, так как завершается его процесс.

п.4 - п.5

<img width="692" height="96" alt="Задача 3 2" src="https://github.com/user-attachments/assets/90da2a9f-e515-4e20-81b6-8c8db7e65a7a" />

п.6
<img width="1287" height="764" alt="Задача 3 4" src="https://github.com/user-attachments/assets/a10a9fb1-3004-43fb-8725-f80ee7b5a2a5" />

п.7

<img width="616" height="780" alt="Задача 3 5" src="https://github.com/user-attachments/assets/f3d3786d-eb08-4f62-a3de-7662f215ed3f" />

п.8 - п.9

<img width="711" height="238" alt="Задача 3 6" src="https://github.com/user-attachments/assets/0c9baee3-6e5e-45aa-ac0f-eef59e873f09" />

п.10

<img width="652" height="122" alt="Задача 3 7" src="https://github.com/user-attachments/assets/484e8be8-f24a-48ed-a210-88766224dc3f" />

Мы поменяли порт, который слуашает nginx, а сопостовление портов запущенного контейнера и хост машины оставили как есть.

п.12
<img width="1352" height="195" alt="Задача 3 8" src="https://github.com/user-attachments/assets/7772a1c9-ade6-45a1-a644-d9e7720dd547" />

## Задача 4

- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку  текущий рабочий каталог ```$(pwd)``` на хостовой машине в ```/data``` контейнера, используя ключ -v.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив текущий рабочий каталог ```$(pwd)``` в ```/data``` контейнера.
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в текущий каталог ```$(pwd)``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

## Ответ

п.1
<img width="1095" height="347" alt="Задача 4 1" src="https://github.com/user-attachments/assets/27db8bd6-7eb0-4b9a-8372-3ad51162939c" />

п.2

<img width="957" height="245" alt="Задача 4 2" src="https://github.com/user-attachments/assets/00b75c51-4cdd-479d-bc62-89194d999a04" />

п.3
<img width="1027" height="382" alt="Задача 4 3" src="https://github.com/user-attachments/assets/b117a912-f2d6-4896-9b31-bcff2939deae" />

п.4 - п.5
<img width="1098" height="1028" alt="Задача 4 4" src="https://github.com/user-attachments/assets/75084d99-39e5-4088-a969-89afefa838c4" />

## Задача 5

1. Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него.
"compose.yaml" с содержимым:
```
version: "3"
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
"docker-compose.yaml" с содержимым:
```
version: "3"
services:
  registry:
    image: registry:2

    ports:
    - "5000:5000"
```

И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )

2. Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)

3. Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/
4. Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)
5. Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local  окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:

```
version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
```
6. Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".

7. Удалите любой из манифестов компоуза(например compose.yaml).  Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.

## Ответ

п.1
<img width="1372" height="432" alt="Задача 5 1" src="https://github.com/user-attachments/assets/ae507802-b710-4b76-8491-c2dc0e862f4b" />

По умолчанию путь к файлу Compose: compose.yaml (предпочтительный) или compose.yml. Compose также поддерживает docker-compose.yaml и docker-compose.yml для обеспечения обратной совместимости с более ранними версиями. Если в рабочем каталоге оба файла, Compose предпочитает compose.yaml.

п.2
<img width="1652" height="692" alt="Задача 5 2" src="https://github.com/user-attachments/assets/1ae6f2e3-9c0d-4f67-9bb8-76e41381b53e" />

п.3
<img width="1216" height="628" alt="Задача 5 3" src="https://github.com/user-attachments/assets/839c2d07-7dd2-4910-8fc1-d4135e88893f" />
<img width="897" height="592" alt="Задача 5 4" src="https://github.com/user-attachments/assets/ee1003f8-9d05-4c6a-90a5-d512bdfc216e" />

п.4
<img width="1802" height="967" alt="Задача 5 5" src="https://github.com/user-attachments/assets/0d81d6d2-dc3b-41fe-a706-caac90ac91f1" />

п.5
<img width="1858" height="997" alt="Задача 5 6" src="https://github.com/user-attachments/assets/023ac09d-8e6e-4e5f-b971-140ffd09133a" />

п.6
<img width="1778" height="765" alt="Задача 5 7" src="https://github.com/user-attachments/assets/3696ee5c-20a3-4546-87d1-341d3f101cae" />
<img width="1798" height="587" alt="Задача 5 8" src="https://github.com/user-attachments/assets/e321c581-2e8b-4d41-a2bd-4a46a7c35178" />

п.7
<img width="1847" height="492" alt="Задача 5 9" src="https://github.com/user-attachments/assets/47cbf98e-57e8-487d-ac06-ece4e3acce59" />
После выполнения команды появилось предупреждение ```Found orphan containers ([task_5-registry-1]) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.```, которое говорит о том, что найдены контейнеры, которые не описаны в файле. Для их очистки нужно выполнить ту же команду(```docker compose up -d```) с флагом --remove-orphans.
