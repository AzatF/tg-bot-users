# tg-bot-users 🤖

# Список команд:

1. [x] **меню** _(Вызов только из групп модераторов.)_
2. [x] **chatinfo** _(Вызов из любой группы, где есть бот администратор. Присылает сообщение с ID и названием группы в админку.)_
3. [x] **moder** _(Вызов из любой группы, где есть бот. Присылает запрос в админку на добавление группы в список
   администраторов. Действует ограничение по времени 60 секунд.)_
4. [x] **Мат** + слово _(Слово будет добавлено в базу, работает только в группах администраторов.) Бот так-же контролирует содержание нецензурных выражений
   в группах, удаляет исходное сообщение, выводит предупреждение в группу. А так-же, присылает оповещение по
   всем группам администраторов с данными нарушителя и копией сообщения._
5. [x] **addmoderatorgroup + ID группы** _(Добавление группы администраторов по ID)_
6. [x] Бот отслеживает вход юбилейных пользователей в группы. Оповещение приходит всем группам администраторов.
   Список всех юбилейных пользователей можно вызвать из **меню администратора**.
7. [x] На большинство административных сообщений действует автоматическая очистка.
