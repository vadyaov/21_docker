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

  - "SizeRw": 1095 - Размер файлов, которые были созданы или изменены в контейнере
  по сравнению с его исходным образом, в байтах. Это представляет собой разницу
  между состоянием файловой системы контейнера и состоянием файловой системы
  исходного образа контейнера.
  - "SizeRootFs": 186738284 - Общий размер всех файлов в контейнере, в байтах.
  Это включает в себя все файлы, как внутри контейнера, так и файлы из исходного
  образа контейнера.


  - список замапленных портов в данный момент является пустым: `HostConfig.PortBindings: {}`

<p align="center">
  <img src="../images/part_1.5.2.png" />
  <p align="center">
    <sup> binding port list </sup>
  </p>
</p>

* **Остановить докер образ через docker stop [container_id|container_name]**

![использование команды docker stop](../images/part_1.6.png)

* **Проверить, что образ остановился через docker ps**

![использование команды docker ps](../images/part_1.7.png)

* **Запустить докер с портами 80 и 443 в контейнере, замапленными на такие же порты на локальной машине, через команду run**

![использование команды docker run](../images/part_1.8.png)

* **Проверить, что в браузере по адресу localhost:80 доступна стартовая страница nginx**

![проверка localhost:80 в браузере](../images/part_1.9.png)

* **Перезапустить докер контейнер через docker restart [container_id|container_name]**

![использование команды docker restart](../images/part_1.10.png)

* **Проверить любым способом, что контейнер запустился**

![использование команды ...](../images/part_1.11.png)

## Part 2. Операции с контейнером
