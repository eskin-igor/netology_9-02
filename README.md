## netology_9-02
### Домашнее задание к занятию «Система мониторинга Zabbix. Часть 1.»

## Задание 1

Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

Требования к результатам  
Прикрепите в файл README.md скриншот авторизации в админке.  
Приложите в файл README.md текст использованных команд в GitHub.

## Решение 1

1. Установите PostgreSQL.
apt install postgresql
2. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.

![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-00.PNG)
а. Установить репозиторий Zabbix:    
   wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian12_all.deb  
   dpkg -i zabbix-release_latest_6.0+debian12_all.deb  
   apt update  
б. Установка Zabbix сервера, интерфейса, агента:  
   apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent  
в. Создать начальную базу данных;  
   Убедитесь, что сервер базы данных запущен и работает.  
   Запустите следующую команду на хосте вашей базы данных.  
   sudo -u postgres createuser --pwprompt zabbix  
   sudo -u postgres createdb -O zabbix zabbix  
   На сервере Zabbix импортируйте начальную схему и данные. Вам будет предложено ввести ваш новый пароль.  
   zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix  
г. Настройте базу данных для Zabbix сервера:  
  Отредактируйте файл /etc/zabbix/zabbix_server.conf  
   DBPassword=password  
д. Запустите процессы Zabbix сервера и агента:  
   Запустите процессы сервера и агента Zabbix и сделайте так, чтобы они запускались при загрузке системы.  
   systemctl restart zabbix-server zabbix-agent apache2  
   systemctl enable zabbix-server zabbix-agent apache2  
е. Откройте веб-страницу Zabbix UI:  
   URL-адрес по умолчанию для Zabbix UI при использовании веб-сервера Apache — http://host/zabbix  

3. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-01.PNG)
![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-02.PNG)
![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-03.PNG)
![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-04.PNG)
![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-05.PNG)
![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-06.PNG)
![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-08.PNG)
![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-01-07.PNG)

## Задание 2

Установите Zabbix Agent на два хоста.

Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Требования к результатам  
Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу.  
Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером.  
Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.  
Приложите в файл README.md текст использованных команд в GitHub.  

## Решение 2

1. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
а. Установить репозиторий Zabbix:  
   wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian12_all.deb  
   dpkg -i zabbix-release_latest_6.0+debian12_all.deb  
   apt update  
б. Установить Zabbix агент:  
   apt install zabbix-agent  
в. Запустить процесс Zabbix агента:  
   systemctl restart zabbix-agent  
   systemctl enable zabbix-agent  
2. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.

![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-02-02.PNG)

3. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.

![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-02-03.PNG)

4. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

![](https://github.com/eskin-igor/netology_9-02/blob/main/screenshots_9-02/9-02-02-04.PNG)

## Задание 3 со звёздочкой*
Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.

Требования к результатам  
Приложите в файл README.md скриншот раздела Latest Data, где видно свободное место на диске C:

## Критерии оценки
1. Выполнено минимум 2 обязательных задания
2. Прикреплены требуемые скриншоты и тексты
3. Задание оформлено в шаблоне с решением и опубликовано на GitHub
