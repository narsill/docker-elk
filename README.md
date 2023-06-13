# docker-elk

репозитории:
* [Elasticsearch](https://github.com/elastic/elasticsearch/tree/main/distribution/docker)
* [Logstash](https://github.com/elastic/logstash/tree/main/docker)
* [Kibana](https://github.com/elastic/kibana/tree/main/src/dev/build/tasks/os_packages/docker_generator)

порты на которых работает ЕLK:

* 5044: Logstash Beats input
* 50000: Logstash TCP input
* 9600: Logstash monitoring API
* 9200: Elasticsearch HTTP
* 9300: Elasticsearch TCP transport
* 5601: Kibana

[Начало работы]

 В терминале запускаем.

> git clone https://github.com/narsill/docker-elk.git

скорее всего придется запускать от суперпользователя:

> docker compose up setup

> docker compose up -d (-d запускает контейнеры в фоновом режиме)

###
Запустите веб-интерфейс Kibana, открыв http://localhost:5601 в веб-браузере, и используйте следующие учетные данные для входа:

Пользователь: elastic

пароль: changeme

[Очистка]

Данные Elasticsearch по умолчанию сохраняются внутри тома.
Чтобы полностью отключить стек и удалить все сохраненные данные, используйте следующую команду Docker Compose:

> docker-compose down -v

Как отключить платные функции.
Измените значение xpack.license.self_generated.typeпараметра Elasticsearch с trialна basic(см. Настройки лицензии ).

[Как повторно выполнить настройку]

Чтобы снова запустить контейнер установки и повторно инициализировать всех пользователей, для которых внутри файла был определен пароль .env, просто снова «включите» 

setup службу Compose:

> docker compose build 
#
Про Filebeat

filebeat это агент который ставится на удаленные машины для передачи логов и другой информации на ЕLK.
установка filebeat:

> dpkg -i <название>.deb

после установки редактируем конф. файл /etc/filebeat/filebeat.yml

> filebeat setup 

раскомменируем строку output logstash и указав ip адрес на котором развернут ELK

так же требуется включить модули

список доступных модулей 

> filebeat modules list

включить нужный модуль 

> filebeat modules <название> enable

после всего можно перезапустить filebeat

> systemctl restart filebeat

