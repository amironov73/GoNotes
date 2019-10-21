### Структура проекта

Вот чем берёт Go – стандартизацией. Язык очень стандартизированный. Начиная с отступов-пробелов, заканчивая структурой проекта. Последняя изложена в репозитории https://github.com/golang-standards/project-layout

#### Папки с G0-кодом
##### /cmd
Главные приложения проекта. Имя папки для каждого приложения должно совпадать с именем самого приложения (например, `/cmd/myapp`). Примеры см. [project-layout/cmd](https://github.com/golang-standards/project-layout/blob/master/cmd/README.md).

##### /internal

Приватные приложения и библиотечный код. Код, который не должен импортироваться другими приложениями или библиотеками.

##### /pkg
Библиотечный код, предназначенный для использования внешними приложениями (например, `/pkg/mypubliclib`). Примеры см. [project-layout/pkg](https://github.com/golang-standards/project-layout/blob/master/pkg/README.md).

##### /vendor

Зависимости приложения, отслеживаемые вручную либо с помощью менеджера пакетов. Не надо коммитить зависимости, если Вы создаёте библиотеку.

#### Служебные папки приложения

#####/api

Спецификации OpenAPI/Swagger, файлы JSON schema, файлы определения протокола. См. примеры [project-layout/api](https://github.com/golang-standards/project-layout/blob/master/api/README.md).

#### Папки веб-приложения

##### /web

Компоненты, специфичные для веб-приложения: статические веб-ассеты, серверные шаблоны и SPA.

#### Общие папки приложения

##### /configs

Шаблоны файлов конфигурации или конфигурационные файлы по умолчанию. Здесь должны быть файлы шаблонов `confd` или `consul-template`.

##### /init

Конфигурации для system init (systemd, upstart, sysv) и менеджера процессов/супервизора (runit, supervisord).

##### /scripts

Различные скрипты, необходимые для сборки проекта, инсталляции и прочих нужд развёртывания приложения. Корневые скрипты для Makefile должны быть маленькими и простыми (пример: https://github.com/hashicorp/terraform/blob/master/Makefile). См. ещё примеры: [project-layout/scripts](https://github.com/golang-standards/project-layout/blob/master/scripts/README.md).

##### /build

Упаковка дистрибутива и Continuous Integration. Сюда помещают файлы настроек для облачных сервисов (AMI), контейнеров (Docker), пакетных менеджеров (deb, rpm, pkg) (всё это богатство собирают в `/build/package`) и скрипты для CI-сервисов (Travis, Circle, Drone и т.д.) (а это — в `/build/ci`). Некоторые сервисы (например, Travis CI) ожидают файлы конфигурации в определённой локации. Можно попробовать сделать link.

##### /deployments

Файлы конфигурации и шаблоны для IaaS, PaaS, оркестрации (docker-compose, kubernetes/helm, mesos, terraform, bosh).

##### /test

Дополнительные внешние тестирующие приложения и данные для тестов. Структурировать их можно по своему вкусу. Примеры см. [project-layout/test](https://github.com/golang-standards/project-layout/blob/master/test/README.md).

#### Прочие папки

##### /docs

Дизайн-документация и руководства пользователя (в дополнение к документации, сгенерированной godoc). Примеры см. [project-layout/docs](https://github.com/golang-standards/project-layout/blob/master/docs/README.md).

##### /tools

Утилиты для данного проекта. Они могут импортировать код из папок `/pkg` и `/internal`. Примеры см. [project-layout/tools](https://github.com/golang-standards/project-layout/blob/master/tools/README.md).

##### /examples

Примеры для вашего приложения и/или публичных библиотек. См. [project-layout/examples](https://github.com/golang-standards/project-layout/blob/master/examples/README.md).

##### /third_party

Внешние утилиты, форкнутый код и прочее (например, Swagger UI).

##### /githooks

Git hooks.

##### /assets

Прочие ресурсы, которые должны быть в репозитории (картинки, логотипы и т.д.).

##### /website
В эту папку помещаются данные веб-сайта проекта, если не используется GitHub pages. Примеры см. [project-layout/website](https://github.com/golang-standards/project-layout/blob/master/website/README.md).

#### Папки, которых не должно быть
##### /src

Разработчики, пришедшие в Go из Java норовят поместить свой код в папку `/src` (например, я так делаю). Не путайте папку `/src` уровня проекта с папкой `src`, которую Go использует для своих рабочих нужд ([How to Write Go Code](https://golang.org/doc/code.html)).

Переменная окружения `$GOPATH` указывает на ваше (текущее) рабочее пространство (по умолчанию она указывает на  `$HOME/go`). Это рабочее пространство включает `/pkg` верхнего уровня, `/bin` и `/src`. Ваш текущий проект всего лишь подпапка в папке `/src`. Так что Вам нужен такой путь: `/some/path/to/workspace/src/your_project/src/your_code.go`. Начиная с Go 1.11 возможно иметь проект вне `GOPATH`.