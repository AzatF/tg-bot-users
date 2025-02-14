# tg-bot-users 🤖

Телеграм бот написан на языке GoLang.   
База данных построена на SQLite3

# Список функций:


1. Бот отслеживает вход юбилейных пользователей в группы. Оповещение приходит связанным группам модераторов. 
   Копия в админку. Возможность поздравить юбилейного пользователя ответным сообщением, есть только у админки.
   Но и из любой группы модераторов можно вызвать список последних юбилейных пользователей и поздравить пользователя.
   (Первое поздравление из админки сделано в целях исключения дублирования нажатия "поздравить" из 
   админки и связанной группы модераторов.)

2. При совпадении ID пользователя в списке юбилейных пользователей в админку приходит уведомление.
3. Список трех последних юбилейных пользователей можно вызвать из **меню администратора**.
4. Список всех юбилейных пользователей можно вызвать из **меню администратора**.
5. Список всех команд можно вызвать из **меню администратора**. Доступно прямое копирование команды нажатием на неё.
6. В меню встроена кнопка "Памятка модераторам", выводит текст в виде сообщения. Текст задается перед запуском в файле конфигурации.
7. Функция фильтрации содержания нецензурных слов в тесте сообщений в группах пользователей.
8. Функция пополнения списка нецензурных слов. Доступно в только в группах модераторов и админке.
9. Функция передачи ID и названия группы автоматическим сообщением в админку.
10. Реализовано несколько вариантов добавления групп модераторов:
    1 - Запрос из любой группы с ботом командой "", запрос приходит в админку, далее принимается решение одобрить или нет.
    2 - Примой командой с номером группы. Доступно из админки.
    3 - При связывании групп модераторов и пользователей, если группа модераторов не найдена в списке доступных.
    (функция добавления группы модераторов без связывания с группами пользователей реализована с целью дальнейшего расширения функционала бота.)
11. Функция просмотра всех групп модераторов и пользователей.
12. Функция фильтрации символов в словах сообщений. Сделано с целью предотвращения маскировки нецензурных слов в сообщениях.
    Пополнить или изменить список символов можно в файле конфигурации.
13. На большинство административных сообщений действует автоматическая очистка.




# Список команд:

1. [x] **меню** _(Вызов только из групп модераторов и админки.)_
2. [x] **chatinfo** _(Вызов из любой группы, где есть бот администратор. Присылает сообщение с ID и названием группы в админку.)_
3. [x] **moder** _(Вызов из любой группы, где есть бот. Присылает запрос в админку на добавление группы в список
   модераторов. Действует ограничение по времени 60 секунд.)_
4. [x] **add-moder-user-link** _(Вызов только из админки. Связывает группу модераторов и пользователей для
   персонализации оповещений о новых пользователях и нецензурных слов в группе.)_
5. [x] **addmoderatorgroup + ID группы** _(Добавление группы модераторов по ID из админки.)_
6. [x] **Мат** + слово _(Слово будет добавлено в базу, работает только в группах администраторов.)_


# Конфигурация приложения:

### Запуск приложения локально: /etc/tgbot/.env

|           ПАРАМЕТР:           |                                            ОПИСАНИЕ:                                            |
|:-----------------------------:|:-----------------------------------------------------------------------------------------------:|
|         TG-BOT-TOKEN          |                         Токен для вашего бота, полученный от BotFather                          |
|         MULTIPLICITY          |                             Кратность выявления новых пользователей                             |
|       TG-BOT-LOG-LEVEL        | Уровень логирования приложения. `panic`, `fatal`, `error`, `warning`, `info`, `debug`, `trace`  |
|       MODERATORS-GROUP        |                                        ID группы админки                                        |
| MSG-OF-BAD-WORDS-TO-USER-CHAT |     Текст который будет выводиться в группу пользователей при обнаружении нецензурных слов      |
|    MSG-TO-CHAT-IF-NEW-USER    |             Текст приветствия в группу при вступлении в группу нового пользователя              |
|     MSG-MODERATOR-MEMBER      |        Текст памятка модераторам. Выводится при нажатии на кнопку `Памятка модераторам`         |
|        MSG-TRIM-SYMBOL        |              Список символов для удаления из строк при проверке слов в сообщениях               |


Клонировать репозиторий, обновить пакеты командой `go mod tidy` , убедиться что все пакеты скачаны и установлены.   
Запуск приложения из папки cmd - go run main.go

# Запуск в Докер-контейнере:

- Команда "make image" создает образ приложения.
---
- Вам нужно создать `volume` под вашу базу данных командой "docker create volume `tgbot_data`"
---
- При первом запуске контейнера вам нужно указать путь к вашей базе данных (`db/path`) и путь к файлу конфигурации, аргументами:
  docker run -v `db/path`:/data -v `env-path`:/etc/tgbot skillbot:latest
---
- Последующие запуски этого контейнера (а так-же последующих с таким же адресом базы) `docker start name`, где `name` это имя контейнера либо его ID, 
  сохранят базу данных предыдущих сеансов работы контейнера.

### Примеры:
```
docker create volume tgbot_data
```
```
make image
```
```
docker run -v /home/user/tgbot_data/:/data -v /home/user/go-projects/telegram_bot_skb/etc/tgbot:/etc/tgbot skillbot:latest 
```
```
docker stop name
```
```
docker start name
```

###  Ссылка на образ:

- [Skillbot v1.0](https://hub.docker.com/repository/docker/azatf/skillbot)