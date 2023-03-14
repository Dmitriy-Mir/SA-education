# PostgreeSQL

### I. Установим на ОС Windows 10.
1. Скачаем с офиц сайта.
1. Установим с учетом некоторых параметров (см. в [видео](https://www.youtube.com/watch?v=PfyC39EzTmk&list=PLPPIc-4tm3YQsdhSV1qzAgDKTuMUNnPmp&index=1)).

### II. Создадим БД и подключимся к ней

1. Запустим PostgreSQL Shell.
Оставляем пустыми Server, Database, Port, Username
и вводим пароль (мы создали его на этапе установки)

![](/PostgreeSQL/screen/1_RunShell.jpg)

2. Проверим кодировку. <br>
Для этого выводим список команд. <br>
Команда: `\?`

![](/PostgreeSQL/screen/2_ASCII.jpg)

Если видим иероглифы, как на скриншоте, то выполняем 1-7 шаги, описанные ниже (в спойлере). Если с кодировкой все впорядке, то пропускаем этот пункт и переходим к [пункту 3](#point3).

<details>
<summary> 1-7 шаги (чтобы исправить кодировку для роботы с PostgreSQL в консоли)</summary>

    1. Сначала нужно добавить путь для команды psql в переменные окружения Windows.
    Щелкните правой кнопкой мыши «Этот компьютер» -> «Свойства» -> «Дополнительные параметры системы» -> «Переменные среды».
    2. В переменную Path добавить путь C:\Program Files\PostgreSQL\15\bin
    3. Перезапустить ПК.
    4. Проверить: запустить cmd, ввести команду 
`psql` 
    
    должно появиться поле с введением логина.

![](/PostgreeSQL/screen/3_cmd.jpg)

    5. Ввести 
`psql -d postgres -U postgres`, где `-d postgres` ключ d и имя БД, `-U postgres`, ключ U и логин.
    
    7.  Ввести команду: 
    
`psql \! chcp 1251`

 и проверить с помощью команды 
 
`\?`

![](/PostgreeSQL/screen/4_ASCII2.jpg)

    Далее работаем в терминале cmd.
    
</details>
<br>

3. <a name="point3"></a> Выведем список текущих таблиц (баз данных): `\l`

![](/PostgreeSQL/screen/5_list_BD.jpg)

4. Создадим базу данных

`CREATE DATABASE nameBD;`

где `nameBD`  это название, которым вы назовете вашу БД.

![](/PostgreeSQL/screen/6_create_BD.jpg)

5. Подключимся к созданной БД

`\c nameBD`
`\coninfo` - информация о подключении

![](/PostgreeSQL/screen/7_open_BD.jpg)

### III. Создадим таблицу и поработаем с ней. 

1. Создадим таблицу "**работник**" - **employee** с такими полями: <br>
**id BIGSERIAL** - самоувеличивающийся идентификатор;  
**first_name VARCHAR(50)** - имя,формат - цифры и буквы, ограничение в 50 символов;  
**last_name VARCHAR(50)** - фамилия;  
**gender VARCHAR(20)** - пол;  
**email VARCHAR(150)** - почта;
**date_of_birth DATE** - дата рождения, форамт "Дата".  

![](/PostgreeSQL/screen/8_crearte_table.jpg)  

1. Информационные команды:  
`\d` - список таблиц;
`\d table_name` - содежимое таблицы.

![](/PostgreeSQL/screen/9_table_info.jpg) 

1. Удалим таблицу **employee**  
`DROP TABLE employee;`  
Также с помощью `DROP` можно удалить базу данных. Поэтому с этой командой нужно быть очень осторожным.

![](/PostgreeSQL/screen/10_drop_table.jpg)

1. Создадим таблицу **работник** снова, но теперь добавим огарничения для ФИО, ид, пол и ДР **NOT NULL** - *не могут быть пустыми*. И для id поставим метку **PRIMARY KEY** - *первичный ключ*.  

![](/PostgreeSQL/screen/11_create_table2.jpg)

1. Добавим первую запись, работник Сергей Ветров, 1990/01/01  

![](/PostgreeSQL/screen/12_create_1string.jpg)

    Но если нужно добавить большой список работников (быстро заполнить таблицу в учебных целях), то это займет много времени. Для упрощения можно использовать сервис mockaroo.com (из РФ через прокси).

1. Открываем сервис [mockaroo](https://mockaroo.com/) 
, создаем список записей для заполнения таблицы с информацией о работниках и скачать файл.

![](/PostgreeSQL/screen/13_create_mockaru.jpg)

1. Дропаем ранее созданную таблицу employee  
`DROP TABLE employee;`

1. Добавляем **NOT NULL** в скачанном с **mockaroo** файле, добавляем **id** и изменяем количество символов для **gender** и **email**.  

![](/PostgreeSQL/screen/14_create_mockaru2.jpg)

1. Импортируем таблицу в свою БД  
`\i C:/Users/.../employee.sql`  

![](/PostgreeSQL/screen/15_create_mockaru_table.jpg)

1. Проверим наполнение командой  
`SELECT * FROM employee;`

![](/PostgreeSQL/screen/16_select_from.jpg)  

### IV. SQL запросы. Выборка данных.  

