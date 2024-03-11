GraphQL API Gateway
===================

GraphQL API шлюз для взаимодействия с микросервисами.

Зависимости
===========
1. Docker для контейнеризации – |link_docker|

.. |link_docker| raw:: html

   <a href="https://www.docker.com" target="_blank">Docker Desktop</a>

2. Для работы с системой контроля версий – |link_git|

.. |link_git| raw:: html

   <a href="https://github.com/git-guides/install-git" target="_blank">Git</a>

3. IDE для работы с исходным кодом – |link_pycharm|

.. |link_pycharm| raw:: html

    <a href="https://www.jetbrains.com/ru-ru/pycharm/download" target="_blank">PyCharm</a>

Установка
=========
1. Клонируйте репозиторий проекта в свою рабочую директорию:

    .. code-block:: console
        git clone https://github.com/katevy/python-course-graphql-gateway.git
Перед началом использования приложения необходимо его сконфигурировать.

.. note::

    Для конфигурации выполните команды, описанные ниже, находясь в корневой директории проекта (на уровне с директорией `src`).

2. Скопируйте файл настроек `.env.sample`, создав файл `.env`:
    .. code-block:: console
        cp .env.sample .env
    Этот файл содержит преднастроенные переменные окружения, значения которых будут общими для всего приложения.
    Файл примера (`.env.sample`) содержит набор переменных со значениями по умолчанию.
    Созданный файл `.env` можно настроить в зависимости от окружения.

    .. warning::

        Никогда не добавляйте в систему контроля версий заполненный файл `.env` для предотвращения компрометации информации о конфигурации приложения.

3. Соберите Docker-контейнер с помощью Docker Compose:
    .. code-block:: console
        docker compose build
    Данную команду необходимо выполнять повторно в случае обновления зависимостей в файле `requirements.txt`.

4. После сборки контейнеров можно их запустить командой:
    .. code-block:: console
        docker compose up
    Данная команда запустит собранные контейнеры для приложения и базы данных.
    Когда запуск завершится, сервер начнет работать по адресу `http://0.0.0.0:8000/graphql.`.


Использование
=============
Пример запроса для получения списка мест:

    .. code-block::graphql
        query {
          places {
            latitude
            longitude
            description
            city
            locality
          }
        }
Пример запроса для получения списка мест с информацией о стране:

    .. code-block::graphql
        query {
          places {
            latitude
            longitude
            description
            city
            locality
            country {
              name
              capital
              alpha2code
              alpha3code
              capital
              region
              subregion
              population
              latitude
              longitude
              demonym
              area
              numericCode
              flag
              currencies
              languages
            }
          }
        }
Пример запроса для получения места:

    .. code-block::graphql
        {
          place(placeId:1) {
            id
            latitude
            longitude
            description
            city
            locality
          }
        }
Пример запроса для создания места:

    .. code-block::graphql
        mutation {
          createPlace (
            latitude: 25.20485,
            longitude: 55.27078,
            description: "Nice food."
          ) {
            place {
              id
              latitude
              longitude
              description
              city
              locality
            }
            result
          }
        }
Пример запроса для обновления данных о месте:

    .. code-block::graphql
        mutation {
          updatePlace (
            placeId: 1,
            latitude: 25.20485,
            longitude: 55.27078,
            description: "updated"
          ) {
            result
          }
        }
Пример запроса для удаления места:

    .. code-block::graphql
        mutation {
          deletePlace(placeId: 1) {
            result
          }
        }


Автоматизация
=============
Проект содержит специальный файл (`Makefile`) для автоматизации выполнения команд:

1. Сборка Docker-контейнера.
2. Генерация документации.
3. Запуск форматирования кода.
4. Запуск статического анализа кода (выявление ошибок типов и форматирования кода).
5. Запуск автоматических тестов.
6. Запуск всех функций поддержки качества кода (форматирование, линтеры, автотесты).

Инструкция по запуску этих команд находится в файле `README.md`.


Тестирование
============
Для запуска автоматических тестов выполните команду:

.. code-block:: console
    make test
Отчет о тестировании находится в файле `src/htmlcov/index.html`.

Документация
============

Клиенты
=======

.. automodule:: clients.base.base
    :members:

.. automodule:: clients.countries
    :members:

.. automodule:: clients.places
    :members:

Модели
======

.. automodule:: models.mixins
    :members:

.. automodule:: models.countries
    :members:

.. automodule:: models.places
    :members:

Схемы
=====

.. automodule:: schema.mutation
    :members:

.. automodule:: schema.query
    :members:

Сервисы
=======

.. automodule:: services.countries
    :members:

.. automodule:: services.places
    :members:
