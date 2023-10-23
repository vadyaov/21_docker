## Part 1. Готовый докер

* **Взять официальный докер образ с nginx и выкачать его при помощи `docker pull`**

<p align="center">
  <img src="../images/part_1.1.png" />
  <p align="center">
    <sup> docker pull command </sup>
  </p>
</p>

* **Проверить наличие докер образа через `docker images`**

<p align="center">
  <img src="../images/part_1.2.png" />
  <p align="center">
    <sup> docker images command </sup>
  </p>
</p>

* **Запустить докер образ через `docker run -d [image_id|repository]`**

<p align="center">
  <img src="../images/part_1.3.png" />
  <p align="center">
    <sup> docker run command </sup>
  </p>
</p>

* **Проверить, что образ запустился через `docker ps`**

<p align="center">
  <img src="../images/part_1.4.png" />
  <p align="center">
    <sup> docker ps command </sup>
  </p>
</p>

* **Посмотреть информацию о контейнере через `docker inspect [container_id|container_name]`**

<p align="center">
  <img src="../images/part_1.5.png" />
  <p align="center">
    <sup> docker inspect command </sup>
  </p>
</p>

* **По выводу команды определить и поместить в отчёт размер контейнера, список замапленных портов и ip контейнера**

Kоманда `docker inspect` не предоставляет информации о размерах контейнера.
Используя `docker inspect -s nginx`, получаем:

<p align="center">
  <img src="../images/part_1.5.1.png" />
  <p align="center">
    <sup> docker inspect -s command </sup>
  </p>
</p>

`"SizeRw": 1095` - Размер файлов, которые были созданы или изменены в контейнере
  по сравнению с его исходным образом, в байтах. Это представляет собой разницу
  между состоянием файловой системы контейнера и состоянием файловой системы
  исходного образа контейнера.

`"SizeRootFs": 186738284` - Общий размер всех файлов в контейнере, в байтах.
  Это включает в себя все файлы, как внутри контейнера, так и файлы из исходного
  образа контейнера.

Cписок замапленных портов в данный момент является пустым: `HostConfig.PortBindings: {}`

<p align="center">
  <img src="../images/part_1.5.2.png" />
  <p align="center">
    <sup> binding port list </sup>
  </p>
</p>

Ip-адрес контейнера находится в поле `NetworkSettings.IPAddress`:

<p align="center">
  <img src="../images/part_1.5.3.png" />
  <p align="center">
    <sup> ip-adress </sup>
  </p>
</p>

`"IPAddress": "172.17.0.2."`

* **Остановить докер образ через docker stop [container_id|container_name]**

* **Проверить, что образ остановился через docker ps**

<p align="center">
  <img src="../images/part_1.6.png" />
  <p align="center">
    <sup> docker stop + docker ps </sup>
  </p>
</p>

* **Запустить докер с портами 80 и 443 в контейнере, замапленными на такие же порты на локальной машине, через команду run**

Для запуска Docker контейнера с портами 80 и 443, замапленными на такие же порты на локальной машине, можно использовать опцию -p: `docker run -p x:y <name>` означает, что порт x контейнера будет замапплен на порт у локальной машины.

<p align="center">
  <img src="../images/part_1.7.png" />
  <p align="center">
    <sup> docker run -p </sup>
  </p>
</p>

* **Проверить, что в браузере по адресу localhost:80 доступна стартовая страница nginx**

<p align="center">
  <img src="../images/part_1.8.png" />
  <p align="center">
    <sup> localhost:80 nginx </sup>
  </p>
</p>

* **Перезапустить докер контейнер через docker restart [container_id|container_name]**

* **Проверить любым способом, что контейнер запустился**

<p align="center">
  <img src="../images/part_1.9.png" />
  <p align="center">
    <sup> docker restart </sup>
  </p>
</p>

## Part 2. Операции с контейнером

* **Прочитать конфигурационный файл nginx.conf внутри докер контейнера через команду exec**

<p align="center">
  <img src="../images/part_2.1.png" />
  <p align="center">
    <sup> docker exec </sup>
  </p>
</p>

* **Создать на локальной машине файл nginx.conf**

* **Настроить в нем по пути /status отдачу страницы статуса сервера nginx**

<p align="center">
  <img src="../images/part_2.2.png" />
  <p align="center">
    <sup> nginx.conf settings </sup>
  </p>
</p>

Этот конфигурационный блок настраивает сервер Nginx на прослушивание порта 80 и
обработку пути /status. Директива `stub_status` позволяет отдавать страницу статуса
сервера Nginx. 

* **Скопировать созданный файл nginx.conf внутрь докер образа через команду docker cp** 

* **Перезапустить nginx внутри докер образа через команду exec**

<p align="center">
  <img src="../images/part_2.3.png" />
  <p align="center">
    <sup> copying and testing </sup>
  </p>
</p>

* **Проверить, что по адресу localhost:80/status отдается страничка со статусом сервера nginx**

Проверил по адресу `127.0.0.1:80/status`, так как при попытке задать `server_name localhost`
происходил конфликт имен.

<p align="center">
  <img src="../images/part_2.4.png" />
  <p align="center">
    <sup> 127.0.0.1/status </sup>
  </p>
</p>

* **Экспортировать контейнер в файл container.tar через команду export**

<p align="center">
  <img src="../images/part_2.5.png" />
  <p align="center">
    <sup> docker export </sup>
  </p>
</p>

* **Остановить контейнер**

<p align="center">
  <img src="../images/part_2.6.png" />
  <p align="center">
    <sup> docker export </sup>
  </p>
</p>

* **Удалить образ через docker rmi [image_id|repository], не удаляя перед этим контейнеры**

<p align="center">
  <img src="../images/part_2.7.png" />
  <p align="center">
    <sup> docker rmi -f </sup>
  </p>
</p>

* **Удалить остановленный контейнер**

<p align="center">
  <img src="../images/part_2.8.png" />
  <p align="center">
    <sup> docker rmi -f </sup>
  </p>
</p>

* **Импортировать контейнер обратно через команду import**

* **Запустить импортированный контейнер**

<p align="center">
  <img src="../images/part_2.9.png" />
  <p align="center">
    <sup> docker import + run </sup>
  </p>
</p>


## Part 3. Мини веб-сервер

* **Написать мини сервер на C и FastCgi, который будет возвращать простейшую
страничку с надписью Hello World!** 

`sudo apt install libfcgi-dev` - разработочный пакет для библиотеки FastCGI,
он включает заголовочные файлы и другие ресурсы, необходимые для разработки
FastCGI-приложений

<p align="center">
  <img src="../images/part_3.1.png" />
  <p align="center">
    <sup> mini C server </sup>
  </p>
</p>

`gcc -o hello_fcgi hello_fcgi.c -lfcgi` - компиляция

* **Запустить написанный мини сервер через spawn-fcgi на порту 8080**

<p align="center">
  <img src="../images/part_3.2.png" />
  <p align="center">
    <sup> bash script for server run </sup>
  </p>
</p>

_Здесь -a указывает IP-адрес, -p указывает порт, и -n указывает путь к
скомпилированному серверу hello_fcgi_

* **Написать свой nginx.conf, который будет проксировать все запросы с 81 порта на 127.0.0.1:8080**

<p align="center">
  <img src="../images/part_3.3.png" />
  <p align="center">
    <sup> nginx.conf </sup>
  </p>
</p>

* **Проверить, что в браузере по localhost:81 отдается написанная вами страничка**

<p align="center">
  <img src="../images/part_3.4.png" />
  <p align="center">
    <sup> Hello World! </sup>
  </p>
</p>

* **Положить файл nginx.conf по пути ./nginx/nginx.conf (это понадобится позже)**

<p align="center">
  <img src="../images/part_3.5.png" />
  <p align="center">
    <sup> move nginx.conf file </sup>
  </p>
</p>

## Part 4. Свой докер

* **Написать свой докер образ, который:**

  - собирает исходники мини сервера на FastCgi из Части 3
  - запускает его на 8080 порту
  - копирует внутрь образа написанный ./nginx/nginx.conf
  - запускает nginx. 

<p align="center">
  <img src="../images/part_4.1.png" />
  <p align="center">
    <sup> Dockerfile </sup>
  </p>
</p>

* **Собрать написанный докер образ через docker build при этом указав имя и тег**

* **Проверить через docker images, что все собралось корректно**

* **Запустить собранный докер образ с маппингом 81 порта на 80 на локальной машине
и маппингом папки ./nginx внутрь контейнера по адресу, где лежат конфигурационные файлы nginx'а**

* **Проверить, что по localhost:80 доступна страничка написанного мини сервера**

<p align="center">
  <img src="../images/part_4.2.png" />
  <p align="center">
    <sup> docker build + images + run with mapping </sup>
  </p>
</p>

* **Дописать в ./nginx/nginx.conf проксирование странички /status, по которой надо отдавать статус сервера nginx**

* **Перезапустить докер образ**

> Если всё сделано верно, то, после сохранения файла и перезапуска контейнера, конфигурационный файл внутри докер образа должен обновиться самостоятельно без лишних действий

* **Проверить, что теперь по localhost:80/status отдается страничка со статусом nginx**

<p align="center">
  <img src="../images/part_4.3.png" />
  <p align="center">
    <sup> adding status using mapping </sup>
  </p>
</p>
