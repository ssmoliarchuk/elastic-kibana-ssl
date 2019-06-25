## Локальная разработка
### docker/docker-compose.yml
* Elasticsarch
http://localhost:9200

* Kibana
http://localhost:5601

Пароли от kibana  и elasticsearch находятся в docker-compose.override.yml

## Структура папок
### ./docker - файлы docker-a
* ./docker/certs - файлы сертификатов Elastic, Kibana, CA
* ./docker/data - волумы prod контейнеров
* ./docker/create-certs.yml - файл генерации сертификатов поредством контейнера elasticsearch
* ./docker/docker-compose.yml - базовый файл 
* ./docker/docker-compose-override.yml - дев файл 
* ./docker/docker-compose-prod.yml - прод файл
* ./docker/kibana.yml - настройки продовской кибаны
* ./docker/instances.yml - настройки для генерации сертификатов в проде 

## Разворачивание в проде
[Мануал по настройке SSL/TLS/HTTPS в ELK](https://www.elastic.co/blog/configuring-ssl-tls-and-https-to-secure-elasticsearch-kibana-beats-and-logstash)
#### 1. Генерирование сертификатов для Elastic/Kibana

```bash
$ docker-compose -f create-certs.yml up
```

После выполнения этой команды создастся папка /certs, в которой будут лежать сертификаты для 2ух node elasticsearch, kibana и CA

[Подробное описание](https://www.elastic.co/guide/en/elasticsearch/reference/current/configuring-tls-docker.html)

#### 2. Настройка .env переменных docker

```bash
$ touch .env
```

После этого заполянем .env по примеру .env.dist

#### 3. Настраиваем нужный проброс портов в docker-compose.prod.yml

#### 4. Запускаем docker-compose

```bash
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up
```
