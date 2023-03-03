# PostgreeSQL

### I. Установить (на ОС Windows 10)
1. Скачать с офиц сайта.
1. Установить с учетом некоторых параметров.
[Источник.](https://www.youtube.com/watch?v=PfyC39EzTmk&list=PLPPIc-4tm3YQsdhSV1qzAgDKTuMUNnPmp&index=1)

### II. Создать БД, Подключиться, Удалить

1. Запустить PostgreSQL Shell.
Оставляем пустыми Server, Database, Port, Username
и вводим пароль (мы создали его на этапе установки)

![](//SA-education/PostgreeSQL/1_RunShell.jpg)

1. Сменить кодеровку, иначе получим иероглифы.
Например, хотим получить список команд
'\?'

![](//SA-education/PostgreeSQL/2_ASCII.jpg)

    1. Сначала нужно добавить путь для команды psql в переменные окружения Windows.
    Щелкните правой кнопкой мыши «Этот компьютер» -> «Свойства» -> «Дополнительные параметры системы» -> «Переменные среды».
    2. В переменную Path добавить путь C:\Program Files\PostgreSQL\15\bin
    3. Перезапустить ПК.
    4. Проверить: запустить cmd, ввести команду 'psql', должно появиться поле с введением логина.

    ![](//SA-education/PostgreeSQL/3_cmd.jpg)

    5. Ввести 'psql -d postgres -U postgres', где '-d postgres' ключ d и имя БД, '-U postgres' ключ U и логин.
    7.  Ввести команду 'psql \! chcp 1251' и проверить с помощью команды '\?'

    ![](//SA-education/PostgreeSQL/4_ASCII2.jpg)

    Далее работаем в терминале cmd.

[Источник.](https://www.youtube.com/watch?v=-vFnDLJ1blg&list=PLPPIc-4tm3YQsdhSV1qzAgDKTuMUNnPmp&index=2)
