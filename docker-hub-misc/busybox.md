# busybox

## Краткий справочник

Поддерживается: [сообщество Docker](https://github.com/docker-library/busybox)

Где получить помощь: [Slack сообщества Docker, сбой сервера, Unix и Linux или StackOverflow](https://dockr.ly/comm-slack)

## Поддерживаемые теги и соответствующие ссылки Dockerfile

Не описано...

## Краткий справочник (продолжение)

Куда обращаться с вопросами: [https://github.com/docker-library/busybox/issues](https://github.com/docker-library/busybox/issues)

Поддерживаемые архитектуры ([подробнее](https://github.com/docker-library/official-images#architectures-other-than-amd64)): [`amd64`](https://hub.docker.com/r/amd64/busybox/), [`arm32v5`](https://hub.docker.com/r/arm32v5/busybox/), [`arm32v6`](https://hub.docker.com/r/arm32v6/busybox/), [`arm32v7`](https://hub.docker.com/r/arm32v7/busybox/), [`arm64v8`](https://hub.docker.com/r/arm64v8/busybox/), [`i386`](https://hub.docker.com/r/i386/busybox/), [`mips64le`](https://hub.docker.com/r/mips64le/busybox/), [`ppc64le`](https://hub.docker.com/r/ppc64le/busybox/), [`riscv64`](https://hub.docker.com/r/riscv64/busybox/), [`s390x`](https://hub.docker.com/r/s390x/busybox/)

Сведения об артефакте опубликованного образа: [repo-info каталог репозитория repos/busybox/directory](https://github.com/docker-library/repo-info/blob/master/repos/busybox) ([history](https://github.com/docker-library/repo-info/commits/master/repos/busybox)) (метаданные изображения, размер передачи и т. д.)

Обновления образа:&#x20;

[official-images repo's `library/busybox` label](https://github.com/docker-library/official-images/issues?q=label%3Alibrary%2Fbusybox)\
[official-images repo's `library/busybox` file](https://github.com/docker-library/official-images/blob/master/library/busybox) ([history](https://github.com/docker-library/official-images/commits/master/library/busybox))

Исходник этого описания: [docs repo's `busybox/` directory](https://github.com/docker-library/docs/tree/master/busybox) ([history](https://github.com/docker-library/docs/commits/master/busybox))

## Что такое busybox? Швейцарский армейский нож встроенного Linux

**BusyBox** занимает на диске от 1 до 5 МБ (в зависимости от варианта) и является очень хорошим компонентом для создания компактных дистрибутивов.

**BusyBox** объединяет крошечные версии многих распространенных утилит UNIX в один небольшой исполняемый файл. Он предоставляет замену большинству утилит, которые вы обычно найдете в GNU **fileutils**, **shellutils** и т. д. Утилиты **BusyBox** обычно имеют меньше опций, чем их полнофункциональные собратья GNU; однако включенные параметры обеспечивают ожидаемую функциональность и ведут себя очень похоже на их аналоги GNU. **BusyBox** предоставляет довольно полную среду для любой небольшой или встроенной системы.

[wikipedia.org/wiki/BusyBox](https://en.wikipedia.org/wiki/BusyBox)

<figure><img src="../.gitbook/assets/logo.png" alt=""><figcaption></figcaption></figure>

## Как использовать этот образ

### Запустить оболочку BusyBox

```bash
$ docker run -it --rm busybox
```

Это перенесет вас в оболочку **sh**, чтобы вы могли делать то, что хотите, внутри системы **BusyBox**.

### Создайте Dockerfile для бинарника

```docker
FROM busybox
COPY ./my-static-binary /my-static-binary
CMD ["/my-static-binary"]
```

Этот **Dockerfile** позволит вам создать минимальный образ для вашего статически скомпилированного двоичного файла. Вам придется скомпилировать двоичный файл в другом месте, например, в другом контейнере. Для более простой альтернативы, такой же крошечной, но ее легче расширить, [см. alpine](https://hub.docker.com/\_/alpine/).

## Варианты образов

Образы **busybox** содержат BusyBox, созданный для различных вариантов «libc» (для сравнения вариантов «libc» у [Eta Labs есть очень хорошая диаграмма](http://www.etalabs.net/compare\_libcs.html), в которой перечислены многие сходства и различия).

Дополнительные сведения об особенностях процесса сборки для каждого варианта см. в файле `Dockerfile.builder` в том же каталоге, что и **Dockerfile** каждого варианта (см. ссылки выше).

### busybox:glibc

[glibc из Debian](https://packages.debian.org/search?searchon=names\&exact=1\&suite=all\&section=all\&keywords=libc6) (который затем включается в образ)

### busybox:uclibc

[uClibc](https://uclibc.org/) через [Buildroot](https://buildroot.org/) (статически скомпилирован)

### busybox:musl

[musl от Alpine](https://pkgs.alpinelinux.org/packages?name=musl) (статически скомпилирован)

## Лицензия

Просмотрите информацию о [лицензии на программное обеспечение](http://www.busybox.net/license.html), содержащееся в этом образе.

Как и все образы **Docker**, они, вероятно, также содержат другое программное обеспечение, которое может быть под другими лицензиями (например, Bash и т. д. из базового дистрибутива, а также любые прямые или косвенные зависимости от основного программного обеспечения).

Некоторая дополнительная информация о лицензии, которая может быть обнаружена автоматически, может быть найдена в [каталоге busybox/ репозитория repo-info](https://github.com/docker-library/repo-info/tree/master/repos/busybox).

Что касается использования любого предварительно созданного образа, пользователь образа несет ответственность за обеспечение того, чтобы любое использование этого образа соответствовало всем соответствующим лицензиям на все программное обеспечение, содержащееся в нем.
