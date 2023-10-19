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
