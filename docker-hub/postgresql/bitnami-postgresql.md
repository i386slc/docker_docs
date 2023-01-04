# bitnami/postgresql

## Что такое PostgreSQL?

PostgreSQL (Postgres) — объектно-реляционная база данных с открытым исходным кодом, известная своей надежностью и целостностью данных. ACID-совместимый, он поддерживает внешние ключи, соединения, представления, триггеры и хранимые процедуры.

[Overview of PostgreSQL](http://www.postgresql.org)

Товарные знаки: этот список программного обеспечения упакован **Bitnami**. Соответствующие товарные знаки, упомянутые в предложении, принадлежат соответствующим компаниям, и их использование не подразумевает какой-либо аффилированности или одобрения.

## TL;DR

```bash
$ docker run --name postgresql bitnami/postgresql:latest
```

### Docker Compose

```bash
$ curl -sSL https://raw.githubusercontent.com/bitnami/containers/main/bitnami/postgresql/docker-compose.yml > docker-compose.yml
$ docker-compose up -d
```

{% hint style="warning" %}
Эта быстрая установка предназначена только для сред разработки. Вам рекомендуется изменить небезопасные учетные данные по умолчанию и проверить доступные параметры конфигурации в **разделе «Конфигурация»** для более безопасного развертывания.
{% endhint %}

## Зачем использовать образы Bitnami?

* **Bitnami** тщательно отслеживает изменения исходного кода и оперативно публикует новые версии этого образа с помощью наших автоматизированных систем.
* С образами **Bitnami** последние исправления ошибок и функции доступны как можно скорее.
* Контейнеры **Bitnami**, виртуальные машины и облачные образы используют одни и те же компоненты и подход к настройке, что позволяет легко переключаться между форматами в зависимости от потребностей вашего проекта.
* Все наши образы основаны на [minideb](https://github.com/bitnami/minideb) — минималистичном образе контейнера на основе **Debian**, который дает вам небольшой базовый образ контейнера и знаком с ведущим дистрибутивом Linux.
* Все образы **Bitnami**, доступные в **Docker Hub**, подписаны [Docker Content Trust (DCT)](https://docs.docker.com/engine/security/trust/content\_trust/). Вы можете использовать `DOCKER_CONTENT_TRUST=1` для проверки целостности образов.
* Образы контейнеров **Bitnami** выпускаются на регулярной основе вместе с последними доступными пакетами распространения.

## Как развернуть PostgreSQL в Kubernetes?

Развертывание приложений **Bitnami** в виде **Helm Charts** — это самый простой способ начать работу с нашими приложениями в **Kubernetes**. Подробнее об установке читайте в [репозитории Bitnami PostgreSQL Chart на GitHub](https://github.com/bitnami/charts/tree/master/bitnami/postgresql).

Контейнеры **Bitnami** можно использовать с Kubeapps для развертывания и управления Helm Charts в кластерах.

## Зачем использовать контейнер без полномочий root?

Образы контейнеров без полномочий **root** добавляют дополнительный уровень безопасности и обычно рекомендуются для производственных сред. Однако, поскольку они выполняются от имени пользователя без полномочий **root**, привилегированные задачи, как правило, запрещены. Узнайте больше о контейнерах без полномочий root в [нашей документации](https://docs.bitnami.com/tutorials/work-with-non-root-containers/).

## Поддерживаемые теги и соответствующие ссылки Dockerfile

Узнайте больше о политике тегов **Bitnami** и о разнице между скользящими тегами и неизменяемыми тегами на нашей [странице документации](https://docs.bitnami.com/tutorials/understand-rolling-tags-containers/).

Вы можете увидеть эквивалентность между различными тегами, взглянув на файл `tags-info.yaml`, находящийся в папке ветки, то есть `bitnami/ASSET/BRANCH/DISTRO/tags-info.yaml`.

Подпишитесь на обновления проекта, просматривая [репозиторий bitnami/containers на GitHub](https://github.com/bitnami/containers).

## Получить этот образ

Рекомендуемый способ получить образ Docker Bitnami PostgreSQL — извлечь готовый образ из [реестра Docker Hub](https://hub.docker.com/r/bitnami/postgresql).

```bash
$ docker pull bitnami/postgresql:latest
```

Чтобы использовать конкретную версию, вы можете извлечь тег версии. Вы можете просмотреть [список доступных версий](https://hub.docker.com/r/bitnami/postgresql/tags/) в реестре Docker Hub.

```bash
$ docker pull bitnami/postgresql:[TAG]
```

При желании вы также можете собрать образ самостоятельно, клонировав репозиторий, перейдя в каталог, содержащий **Dockerfile**, и выполнив команду сборки `docker build`. Не забудьте заменить заполнители пути **APP**, **VERSION** и **OPERATING-SYSTEM** в приведенном ниже примере команды правильными значениями.

```bash
$ git clone https://github.com/bitnami/containers.git
$ cd bitnami/APP/VERSION/OPERATING-SYSTEM
$ docker build -t bitnami/APP:latest .
```

## Сохранение вашей базы данных

Если вы удалите контейнер, все ваши данные и конфигурации будут потеряны, а при следующем запуске образа база данных будет повторно инициализирована. Чтобы избежать этой потери данных, вы должны смонтировать том, который будет сохраняться даже после удаления контейнера.

Для сохранения вы должны смонтировать каталог по пути `/bitnami/postgresql`. Если смонтированный каталог пуст, он будет инициализирован при первом запуске.

```bash
$ docker run \
    -v /path/to/postgresql-persistence:/bitnami/postgresql \
    bitnami/postgresql:latest
```

или изменив файл [docker-compose.yml](https://github.com/bitnami/containers/tree/main/bitnami/postgresql/docker-compose.yml) в этом репозитории:

```yaml
services:
  postgresql:
  ...
    volumes:
      - /path/to/postgresql-persistence:/bitnami/postgresql
  ...
```

{% hint style="info" %}
Поскольку это контейнер без полномочий **root**, смонтированные файлы и каталоги должны иметь соответствующие разрешения для `UID 1001`.
{% endhint %}

## Подключение к другим контейнерам

Используя [сеть контейнеров Docker](https://docs.docker.com/engine/userguide/networking/), контейнеры приложений могут легко получить доступ к серверу **PostgreSQL**, работающему внутри контейнера.

Контейнеры, подключенные к одной сети, могут взаимодействовать друг с другом, используя имя контейнера в качестве имени хоста.

### Использование командной строки

В этом примере мы создадим экземпляр клиента **PostgreSQL**, который будет подключаться к экземпляру сервера, работающему в той же сети докеров, что и клиент.

#### Шаг 1. Создание сети

```bash
$ docker network create app-tier --driver bridge
```

#### Шаг 2. Запуск экземпляра сервера PostgreSQL

Используйте аргумент **--network** уровня приложения для команды запуска `docker run`, чтобы подключить контейнер **PostgreSQL** к сети уровня приложения.

```bash
$ docker run -d --name postgresql-server \
    --network app-tier \
    bitnami/postgresql:latest
```

#### Шаг 3. Запуск экземпляр клиента PostgreSQL

Наконец, мы создаем новый экземпляр контейнера для запуска клиента **PostgreSQL** и подключения к серверу, созданному на предыдущем шаге:

```bash
$ docker run -it --rm \
    --network app-tier \
    bitnami/postgresql:latest psql -h postgresql-server -U postgres
```

### Использование Docker Compose

Если не указано иное, **Docker Compose** автоматически настраивает новую сеть и подключает к ней все развернутые службы. Однако мы явно определим новую мостовую сеть с именем **app-tier**. В этом примере мы предполагаем, что вы хотите подключиться к серверу **PostgreSQL** из своего собственного пользовательского образа приложения, которое в следующем фрагменте кода обозначено именем службы **myapp**.

```yaml
version: '2'

networks:
  app-tier:
    driver: bridge

services:
  postgresql:
    image: 'bitnami/postgresql:latest'
    networks:
      - app-tier
  myapp:
    image: 'YOUR_APPLICATION_IMAGE'
    networks:
      - app-tier
```

{% hint style="info" %}
1. Обновите заполнитель **YOUR\_APPLICATION\_IMAGE\_** в приведенном выше фрагменте образа вашего приложения.
2. В контейнере приложения используйте имя хоста **postgresql** для подключения к серверу **PostgreSQL**.
{% endhint %}

Запустите контейнеры, используя:

```bash
$ docker-compose up -d
```

## Конфигурация

### При запуске контейнера

Когда контейнер будет запущен, он выполнит файлы с расширением `.sh`, расположенные в `/docker-entrypoint-preinitdb.d`, перед инициализацией или запуском **postgresql**.

Чтобы ваши пользовательские файлы были внутри образа докера, вы можете смонтировать их как том.

### Передача дополнительных флагов командной строки в PostgreSQL

Передача дополнительных флагов командной строки сервисной команде **postgresql** возможна через следующую переменную окружения:

* **POSTGRESQL\_EXTRA\_FLAGS**: флаги, добавляемые к команде запуска **postgres**. Нет значений по умолчанию

### Инициализация нового экземпляра

При первом запуске контейнера будут выполняться файлы с расширениями `.sh`, `.sql` и **.sql.gz**, расположенные в `/docker-entrypoint-initdb.d`.

Чтобы ваши пользовательские файлы были внутри образа докера, вы можете смонтировать их как том.

### Установка пароля root при первом запуске

В приведенных выше командах вы могли заметить использование переменной среды **POSTGRESQL\_PASSWORD**. Передача переменной среды **POSTGRESQL\_PASSWORD** при первом запуске образа установит для пароля пользователя **postgres** в значение **POSTGRESQL\_PASSWORD** (или содержимое файла, указанного в **POSTGRESQL\_PASSWORD\_FILE**).

```bash
$ docker run --name postgresql \
        -e POSTGRESQL_PASSWORD=password123 \
        bitnami/postgresql:latest
```

или изменив файл [docker-compose.yml](https://github.com/bitnami/containers/tree/main/bitnami/postgresql/docker-compose.yml) в этом репозитории:

```yaml
services:
  postgresql:
  ...
    environment:
      - POSTGRESQL_PASSWORD=password123
  ...
```

{% hint style="info" %}
Пользователь **postgres** является **суперпользователем** и имеет полный административный доступ к базе данных **PostgreSQL**.
{% endhint %}

См. [Создание пользователя базы данных при первом запуске](bitnami-postgresql.md#sozdanie-polzovatelya-bazy-dannykh-pri-pervom-zapuske), если вы хотите установить непривилегированного пользователя и пароль для пользователя **postgres**.

### Создание базы данных при первом запуске

Передав переменную среды **POSTGRESQL\_DATABASE** при первом запуске образа, будет создана база данных. Это полезно, если вашему приложению требуется, чтобы база данных уже существовала, что избавляет вас от необходимости вручную создавать базу данных с помощью клиента **PostgreSQL**.

```bash
$ docker run --name postgresql \
        -e POSTGRESQL_DATABASE=my_database \
        bitnami/postgresql:latest
```

или изменив файл [docker-compose.yml](https://github.com/bitnami/containers/tree/main/bitnami/postgresql/docker-compose.yml) в этом репозитории:

```yaml
services:
  postgresql:
  ...
    environment:
      - POSTGRESQL_DATABASE=my_database
  ...
```

### Создание пользователя базы данных при первом запуске

Вы также можете создать ограниченного пользователя базы данных, у которого есть разрешения только для базы данных, созданной с помощью переменной среды [POSTGRESQL\_DATABASE](bitnami-postgresql.md#sozdanie-bazy-dannykh-pri-pervom-zapuske). Для этого укажите переменную среды **POSTGRESQL\_USERNAME**.

```bash
$ docker run --name postgresql \
        -e POSTGRESQL_USERNAME=my_user \
        -e POSTGRESQL_PASSWORD=password123 \
        -e POSTGRESQL_DATABASE=my_database \
        bitnami/postgresql:latest
```

или изменив файл [docker-compose.yml](https://github.com/bitnami/containers/tree/main/bitnami/postgresql/docker-compose.yml) в этом репозитории:

```yaml
services:
  postgresql:
  ...
    environment:
      - POSTGRESQL_USERNAME=my_user
      - POSTGRESQL_PASSWORD=password123
      - POSTGRESQL_DATABASE=my_database
  ...
```

{% hint style="info" %}
Когда указано **POSTGRESQL\_USERNAME**, пользователю **postgres** не назначается пароль, и в результате вы не можете удаленно войти на сервер **PostgreSQL** как пользователь **postgres**. Если вы все еще хотите иметь доступ с пользователем **postgres**, установите переменную среды **POSTGRESQL\_POSTGRES\_PASSWORD** (или содержимое файла, указанного в **POSTGRESQL\_POSTGRES\_PASSWORD\_FILE**).
{% endhint %}

### Аудит

Образ **Bitnami PostgreSQL** поставляется с включенным по умолчанию модулем **pgAudit**. Благодаря этому информация аудита может быть включена в контейнере с этими переменными среды:

* **POSTGRESQL\_PGAUDIT\_LOG**: список, разделенный запятыми, с различными операциями для аудита. Найдите в [официальной документации pgAudit](https://github.com/pgaudit/pgaudit#configuration) список возможных значений. Нет значений по умолчанию.
* **POSTGRESQL\_PGAUDIT\_LOG\_CATALOG**: ведение журнала сеансов включено в случае, если все отношения в операторе находятся в **pg\_catalog**. Нет значений по умолчанию.
* **POSTGRESQL\_LOG\_CONNECTIONS**: добавить запись журнала для входа в систему. Нет значений по умолчанию.
* **POSTGRESQL\_LOG\_DISCONNECTIONS**: добавить запись в журнал для выходов. Нет значений по умолчанию.
* **POSTGRESQL\_LOG\_HOSTNAME**: Запишите имя хоста клиента. Нет значений по умолчанию.&#x20;
* **POSTGRESQL\_LOG\_LINE\_PREFIX**: определите формат строк записи журнала. Найдите в [официальной документации PostgreSQL](https://www.postgresql.org/docs/current/runtime-config-logging.html) строковые параметры. Нет значений по умолчанию.
* **POSTGRESQL\_LOG\_TIMEZONE**: установите часовой пояс для временной метки записи журнала. Нет значений по умолчанию.

### Параметры сессии

Образ **Bitnami PostgreSQL** позволяет настроить несколько параметров для подключения и управления сеансом:

* **POSTGRESQL\_USERNAME\_CONNECTION\_LIMIT**: если создается пользователь, отличный от **postgres**, установите ограничение на количество подключений. Нет значений по умолчанию.
* **POSTGRESQL\_POSTGRES\_CONNECTION\_LIMIT**: установите лимит подключений для пользователя **postgres**. Нет значений по умолчанию.
* **POSTGRESQL\_STATEMENT\_TIMEOUT**: установите время ожидания инструкции. Нет значений по умолчанию.
* **POSTGRESQL\_TCP\_KEEPALIVES\_INTERVAL**: интервал проверки активности TCP. Нет значений по умолчанию.
* **POSTGRESQL\_TCP\_KEEPALIVES\_IDLE**: время простоя проверки активности TCP. Нет значений по умолчанию.
* **POSTGRESQL\_TCP\_KEEPALIVES\_COUNT**: счетчик поддержки активности TCP. Нет значений по умолчанию.

### Настройка часового пояса

Образ **Bitnami PostgreSQL** позволяет настроить часовой пояс для **PostgreSQL** со следующими переменными среды:

* **POSTGRESQL\_TIMEZONE**: устанавливает часовой пояс для отображения и интерпретации временных меток.
* **POSTGRESQL\_LOG\_TIMEZONE**: устанавливает часовой пояс, используемый для отметок времени, записываемых в журнал сервера.

### Изменение pg\_hba.conf

По умолчанию образ **Bitnami PostgreSQL** создает локальные записи **local** и записи **md5** в файле **pg\_hba.conf**. Чтобы адаптироваться к любым другим требованиям или стандартам, можно изменить файл **pg\_hba.conf** следующим образом:

* Примонтируйте собственный файл **pg\_hba.conf** в `/bitnami/postgresql/conf`
* Используйте **POSTGRESQL\_PGHBA\_REMOVE\_FILTERS** со списком шаблонов, разделенных запятыми. Все строки, соответствующие любому из шаблонов, будут удалены. Например, если мы хотим удалить всю локальную аутентификацию **local** и аутентификацию **md5** (например, в пользу соединений только **hostssl**), установите `POSTGRESQL_PGHBA_REMOVE_FILTERS=local, md5`.

### Предварительная загрузка общих библиотек

Можно изменить список библиотек, которые **PostgreSQL** будет предварительно загружать во время загрузки, установив в файле **POSTGRESQL\_SHARED\_PRELOAD\_LIBRARIES**. Значение по умолчанию — `POSTGRESQL_SHARED_PRELOAD_LIBRARIES=pgaudit`. Если, например, вы хотите добавить в предварительную загрузку библиотеку **pg\_stat\_statements**, установите `POSTGRESQL_SHARED_PRELOAD_LIBRARIES=pgaudit, pg_stat_statements`.

### Настройка потоковой репликации

Кластер [потоковой репликации](http://www.postgresql.org/docs/9.4/static/warm-standby.html#STREAMING-REPLICATION) можно легко настроить с помощью образа **Docker Bitnami PostgreSQL**, используя следующие переменные среды:

* **POSTGRESQL\_REPLICATION\_MODE**: режим репликации. Возможные значения `master/slave`. Нет значений по умолчанию.
* **POSTGRESQL\_REPLICATION\_USER**: пользователь репликации, созданный на **master** при первом запуске. Нет значений по умолчанию.
* **POSTGRESQL\_REPLICATION\_PASSWORD**: пароль пользователя репликации. Нет значений по умолчанию.
* **POSTGRESQL\_REPLICATION\_PASSWORD\_FILE**: путь к файлу, содержащему пароль пользователя репликации. Это переопределит значение, указанное в **POSTGRESQL\_REPLICATION\_PASSWORD**. Нет значений по умолчанию.
* **POSTGRESQL\_MASTER\_HOST**: имя хоста/IP-адрес мастера репликации (параметр ведомого). Нет значений по умолчанию.
* **POSTGRESQL\_MASTER\_PORT\_NUMBER**: порт сервера мастера репликации (параметр ведомого). По умолчанию **5432**.

В кластере репликации у вас может быть один главный и ноль или более подчиненных. Когда репликация включена, главный узел находится в режиме чтения-записи, а подчиненные — в режиме только чтения. Для лучшей производительности рекомендуется ограничить чтение ведомыми устройствами.

#### Шаг 1. Создайте мастер репликации

Первым шагом является запуск мастера.

```bash
$ docker run --name postgresql-master \
  -e POSTGRESQL_REPLICATION_MODE=master \
  -e POSTGRESQL_USERNAME=my_user \
  -e POSTGRESQL_PASSWORD=password123 \
  -e POSTGRESQL_DATABASE=my_database \
  -e POSTGRESQL_REPLICATION_USER=my_repl_user \
  -e POSTGRESQL_REPLICATION_PASSWORD=my_repl_password \
  bitnami/postgresql:latest
```

В этой команде мы настраиваем контейнер как главный, используя параметр `POSTGRESQL_REPLICATION_MODE=master`. Пользователь репликации указывается с помощью параметров **POSTGRESQL\_REPLICATION\_USER** и **POSTGRESQL\_REPLICATION\_PASSWORD**.

#### Шаг 2: Создайте ведомое устройство репликации

Затем мы запускаем подчиненный контейнер репликации.

```bash
$ docker run --name postgresql-slave \
  --link postgresql-master:master \
  -e POSTGRESQL_REPLICATION_MODE=slave \
  -e POSTGRESQL_MASTER_HOST=master \
  -e POSTGRESQL_MASTER_PORT_NUMBER=5432 \
  -e POSTGRESQL_REPLICATION_USER=my_repl_user \
  -e POSTGRESQL_REPLICATION_PASSWORD=my_repl_password \
  bitnami/postgresql:latest
```

В приведенной выше команде контейнер настраивается как подчиненный с помощью параметра **POSTGRESQL\_REPLICATION\_MODE**. Перед запуском ведомого устройства репликации параметры **POSTGRESQL\_MASTER\_HOST** и **POSTGRESQL\_MASTER\_PORT\_NUMBER** используются ведомым контейнером для подключения к ведущему и репликации исходной базы данных с ведущего. Учетные данные **POSTGRESQL\_REPLICATION\_USER** и **POSTGRESQL\_REPLICATION\_PASSWORD** используются для аутентификации с мастером. Чтобы изменить настройки по умолчанию `pg_hba.conf`, ведомому устройству необходимо знать, установлен ли **POSTGRESQL\_PASSWORD**.

С помощью этих двух команд у вас теперь есть кластер потоковой репликации **PostgreSQL** `master-slave` с двумя узлами, работающий и работающий. Вы можете масштабировать кластер, добавляя/удаляя ведомые устройства без простоев.

{% hint style="info" %}
Кластер полностью реплицирует мастер, включая всех пользователей и базы данных.
{% endhint %}

Если мастер выходит из строя, вы можете перенастроить подчиненное устройство, чтобы оно действовало как мастер, и начать принимать записи, создав файл триггера `/tmp/postgresql.trigger.5432`. Например, следующая команда перенастраивает **postgresql-slave**, чтобы он действовал как главный:

```bash
$ docker exec postgresql-slave touch /tmp/postgresql.trigger.5432
```

{% hint style="info" %}
Конфигурацию других подчиненных устройств в кластере необходимо обновить, чтобы они знали о новом главном устройстве. Для этого вам потребуется перезапустить другие ведомые устройства с помощью `--link postgresql-slave:master`, как в наших примерах.
{% endhint %}

С помощью **Docker Compose** репликацию **master-slave** можно настроить с помощью:

```yaml
version: '2'

services:
  postgresql-master:
    image: 'bitnami/postgresql:latest'
    ports:
      - '5432'
    volumes:
      - 'postgresql_master_data:/bitnami/postgresql'
    environment:
      - POSTGRESQL_REPLICATION_MODE=master
      - POSTGRESQL_REPLICATION_USER=repl_user
      - POSTGRESQL_REPLICATION_PASSWORD=repl_password
      - POSTGRESQL_USERNAME=my_user
      - POSTGRESQL_PASSWORD=my_password
      - POSTGRESQL_DATABASE=my_database
  postgresql-slave:
    image: 'bitnami/postgresql:latest'
    ports:
      - '5432'
    depends_on:
      - postgresql-master
    environment:
      - POSTGRESQL_REPLICATION_MODE=slave
      - POSTGRESQL_REPLICATION_USER=repl_user
      - POSTGRESQL_REPLICATION_PASSWORD=repl_password
      - POSTGRESQL_MASTER_HOST=postgresql-master
      - POSTGRESQL_PASSWORD=my_password
      - POSTGRESQL_MASTER_PORT_NUMBER=5432

volumes:
  postgresql_master_data:
```

Масштабируйте количество ведомых устройств, используя:

```bash
$ docker-compose up --detach --scale postgresql-master=1 --scale postgresql-slave=3
```

Приведенная выше команда увеличивает количество ведомых устройств до 3. Таким же образом можно уменьшить масштаб.

{% hint style="info" %}
Вы не должны увеличивать/уменьшать количество мастер-нод. Всегда должен работать только один главный узел.
{% endhint %}

#### Синхронные коммиты

По умолчанию подчиненные экземпляры настроены на асинхронную репликацию. Чтобы гарантировать большую стабильность данных (за счет некоторой производительности), можно установить синхронную фиксацию (т. е. фиксация транзакции не будет возвращать успех клиенту, пока она не будет записана в набор реплик), используя следующие переменные среды.

* **POSTGRESQL\_SYNCHRONOUS\_COMMIT\_MODE**: устанавливает тип синхронной фиксации. Доступные опции: `on`, `remote_apply`, `remote_write`, `local` и `off`. Значение по умолчанию `on`. Для получения дополнительной информации ознакомьтесь с [официальной документацией PostgreSQL](https://www.postgresql.org/docs/9.6/runtime-config-wal.html#GUC-SYNCHRONOUS-COMMIT).
* **POSTGRESQL\_NUM\_SYNCHRONOUS\_REPLICAS**: устанавливает количество реплик, которые будут включать синхронную репликацию. Это число не должно превышать количество подчиненных устройств, которое вы настраиваете в кластере.

С помощью **Docker Compose** репликацию **master-slave** с синхронными фиксациями можно настроить следующим образом:

```yaml
version: '2'

services:
  postgresql-master:
    image: 'bitnami/postgresql:latest'
    ports:
      - '5432'
    volumes:
      - 'postgresql_master_data:/bitnami/postgresql'
    environment:
      - POSTGRESQL_REPLICATION_MODE=master
      - POSTGRESQL_REPLICATION_USER=repl_user
      - POSTGRESQL_REPLICATION_PASSWORD=repl_password
      - POSTGRESQL_USERNAME=my_user
      - POSTGRESQL_PASSWORD=my_password
      - POSTGRESQL_DATABASE=my_database
      - POSTGRESQL_SYNCHRONOUS_COMMIT_MODE=on
      - POSTGRESQL_NUM_SYNCHRONOUS_REPLICAS=1
    volumes:
      - '/path/to/postgresql-persistence:/bitnami/postgresql'
  postgresql-slave:
    image: 'bitnami/postgresql:latest'
    ports:
      - '5432'
    depends_on:
      - postgresql-master
    environment:
      - POSTGRESQL_REPLICATION_MODE=slave
      - POSTGRESQL_REPLICATION_USER=repl_user
      - POSTGRESQL_REPLICATION_PASSWORD=repl_password
      - POSTGRESQL_MASTER_HOST=postgresql-master
      - POSTGRESQL_MASTER_PORT_NUMBER=5432
  postgresql-slave2:
    image: 'bitnami/postgresql:latest'
    ports:
      - '5432'
    depends_on:
      - postgresql-master
    environment:
      - POSTGRESQL_REPLICATION_MODE=slave
      - POSTGRESQL_REPLICATION_USER=repl_user
      - POSTGRESQL_REPLICATION_PASSWORD=repl_password
      - POSTGRESQL_MASTER_HOST=postgresql-master
      - POSTGRESQL_MASTER_PORT_NUMBER=5432
```

В приведенном выше примере коммиты должны быть записаны как на ведущем, так и на одном из ведомых устройств, чтобы быть принятыми. Другое ведомое устройство будет продолжать использовать асинхронную репликацию. Проверьте это с помощью следующего SQL-запроса:

```bash
postgres=# select application_name as server, state,
postgres-#       sync_priority as priority, sync_state
postgres-#       from pg_stat_replication;
| server      | state     | priority | sync_state |
|-------------|-----------|----------|------------|
| walreceiver | streaming | 0        | sync       |
| walreceiver | streaming | 0        | async      |
```

{% hint style="info" %}
Для более сложных настроек вы можете определить разные группы репликации с помощью параметра **application\_name**, установив переменную среды **POSTGRESQL\_CLUSTER\_APP\_NAME**.
{% endhint %}

## LDAP-аутентификация

Чтобы использовать аутентификацию **LDAP**, вам необходимо включить ее, установив для переменной среды **POSTGRESQL\_ENABLE\_LDAP** значение **yes**.

Существует два способа настройки конфигурации **LDAP**:

* Настроив **POSTGRESQL\_LDAP\_URL**, вы можете настроить все связанные параметры в URL-адресе.
* Настройка параметров `POSTGRESQL_LDAP_xxxx` самостоятельно.

Параметры, связанные с **LDAP**:

* **POSTGRESQL\_LDAP\_SERVER**: IP-адреса или имена серверов **LDAP** для подключения. Разделенные пробелами.
* **POSTGRESQL\_LDAP\_PORT**: номер порта на сервере **LDAP** для подключения.
* **POSTGRESQL\_LDAP\_SCHEME**: установите значение **ldaps** для использования **LDAPS**. По умолчанию нет.
* **POSTGRESQL\_LDAP\_TLS**: установите значение 1, чтобы использовать шифрование **TLS**. По умолчанию нет.
* **POSTGRESQL\_LDAP\_PREFIX**: строка, которая добавляется к имени пользователя при формировании DN для привязки. По умолчанию нет.
* **POSTGRESQL\_LDAP\_SUFFIX**: строка, добавляемая к имени пользователя при формировании DN для привязки. По умолчанию нет.
* **POSTGRESQL\_LDAP\_BASE\_DN**: корневое DN, с которого начинается поиск пользователя. По умолчанию — нет.
* **POSTGRESQL\_LDAP\_BIND\_DN**: DN пользователя для привязки к **LDAP**. По умолчанию нет.
* **POSTGRESQL\_LDAP\_BIND\_PASSWORD**: пароль пользователя для привязки к **LDAP**. По умолчанию нет.
* **POSTGRESQL\_LDAP\_SEARCH\_ATTR**: атрибут для сопоставления с именем пользователя в поиске. По умолчанию нет.
* **POSTGRESQL\_LDAP\_SEARCH\_FILTER**: поисковый фильтр, используемый при проверке подлинности поиск + привязка. По умолчанию нет.
* **POSTGRESQL\_LDAP\_URL**: URL-адрес для подключения в формате: `ldap[s]://host[:port]/basedn[?[attribute][?[scope][?[filter]]]]` .

Дополнительные сведения см. в [документации по настройке аутентификации Postgresql LDAP](https://www.postgresql.org/docs/12/auth-ldap.html).

## Защита трафика PostgreSQL

**PostgreSQL** поддерживает шифрование соединений с использованием протокола **SSL/TLS**. Если вы хотите включить эту дополнительную функцию, вы можете использовать следующие переменные среды для настройки приложения:

* **POSTGRESQL\_ENABLE\_TLS**: включать ли TLS для трафика или нет. По умолчанию `'no'`
* **POSTGRESQL\_TLS\_CERT\_FILE**: файл, содержащий файл сертификата для трафика TLS. Нет значений по умолчанию.
* **POSTGRESQL\_TLS\_KEY\_FILE**: файл, содержащий ключ для сертификата. Нет значений по умолчанию.
* **POSTGRESQL\_TLS\_CA\_FILE**: файл, содержащий CA сертификата. Если он предоставлен, PostgreSQL будет аутентифицировать клиентов TLS/SSL, запрашивая у них сертификат (см. [ссылку](https://www.postgresql.org/docs/9.6/auth-methods.html)). Нет значений по умолчанию.
* **POSTGRESQL\_TLS\_CRL\_FILE**: файл, содержащий список отозванных сертификатов. Нет значений по умолчанию.
* **POSTGRESQL\_TLS\_PREFER\_SERVER\_CIPHERS**: следует ли использовать настройки шифрования TLS сервера, а не клиента. По умолчанию **yes**.

При включении TLS PostgreSQL по умолчанию будет поддерживать как стандартный, так и зашифрованный трафик, но предпочитает последний. Ниже приведены несколько примеров того, как быстро настроить трафик TLS:

1. Используя `docker run`

```bash
$ docker run \
    -v /path/to/certs:/opt/bitnami/postgresql/certs \
    -e ALLOW_EMPTY_PASSWORD=yes \
    -e POSTGRESQL_ENABLE_TLS=yes \
    -e POSTGRESQL_TLS_CERT_FILE=/opt/bitnami/postgresql/certs/postgres.crt \
    -e POSTGRESQL_TLS_KEY_FILE=/opt/bitnami/postgresql/certs/postgres.key \
    bitnami/postgresql:latest
```

2\. Изменяя файл **docker-compose.yml** в этом репозитории:

```yaml
services:
  postgresql:
  ...
    environment:
      ...
      - POSTGRESQL_ENABLE_TLS=yes
      - POSTGRESQL_TLS_CERT_FILE=/opt/bitnami/postgresql/certs/postgres.crt
      - POSTGRESQL_TLS_KEY_FILE=/opt/bitnami/postgresql/certs/postgres.key
    ...
    volumes:
      ...
      - /path/to/certs:/opt/bitnami/postgresql/certs
  ...
```

Кроме того, вы также можете указать эту конфигурацию в своем [пользовательском файле](bitnami-postgresql.md#fail-konfiguracii) конфигурации.

## Файл конфигурации

{% hint style="info" %}
**README** для этого образа длиннее предела длины **DockerHub**, равного 25000, поэтому он был обрезан. Полный **README** можно найти по адресу [https://github.com/bitnami/containers/blob/main/bitnami/postgresql/README.md](https://github.com/bitnami/containers/blob/main/bitnami/postgresql/README.md).
{% endhint %}
