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

![](/PostgreeSQL/screen/8_create_table.jpg)  

2. Информационные команды:  
`\d` - список таблиц;  
`\d table_name` - содежимое таблицы.

![](/PostgreeSQL/screen/9_table_info.jpg) 

3. Удалим таблицу **employee**  
`DROP TABLE employee;`  

![](/PostgreeSQL/screen/10_drop_table.jpg)  

    Также с помощью `DROP` можно удалить базу данных. Поэтому с этой командой нужно быть очень осторожным.

4. Создадим таблицу **работник** снова, но теперь добавим огарничения для ФИО, ид, пол и ДР **NOT NULL** - *не могут быть пустыми*. И для id поставим метку **PRIMARY KEY** - *первичный ключ*.   

![](/PostgreeSQL/screen/12_create_table2.jpg)

5. Добавим первую запись, работник **Сергей Ветров, 1990/01/01**  

![](/PostgreeSQL/screen/11_create_1string.jpg)

    Но если нужно добавить большой список работников (быстро заполнить таблицу в учебных целях), то это займет много времени.  
    Для упрощения можно использовать сервис mockaroo.com (из РФ через прокси).

6. Открываем сервис [mockaroo](https://mockaroo.com/) 
, создаем список записей для заполнения таблицы с информацией о работниках и скачать файл.

![](/PostgreeSQL/screen/13_create_mockaru.jpg)

7. Дропаем ранее созданную таблицу employee  
`DROP TABLE employee;`

8. Добавляем **NOT NULL** в скачанном с **mockaroo** файле, добавляем **id** и изменяем количество символов для **gender** и **email**.  

![](/PostgreeSQL/screen/14_create_mockaru2.jpg)

9. Импортируем таблицу в свою БД  
`\i C:/Users/.../employee.sql`  

![](/PostgreeSQL/screen/15_create_mockaru_table.jpg)

10. Проверим наполнение командой  
`SELECT * FROM employee;`

![](/PostgreeSQL/screen/16_select_from.jpg)  

### IV. SQL запросы. Выборка данных.  

**SELECT** - вывод данных.  
`SELECT * FROM employee;` - вывод данных всей таблицы, `*` - означает **all** (все);  
`SELECT first_name, last_name FROM employee;` - выведем из таблицы **employee** столбцы с именем и фамилией;  

**ORDER BY** - сортировка.  
`SELECT * FROM employee ORDER BY last_name;` - выведем всю таблицу отсортированную в порядке увеличения (от меншего к большему - такая сортировка идет всегда по умолчанию, если не задать особых условий) по столбцу last_name;  
`SELECT * FROM employee ORDER BY last_name DESC;` - сортировка в обратном порядке;  

**DISTINCT** - вывести только уникальные значения.  
`SELECT DISTINCT gender FROM employee ORDER BY gender;` - выведем пол, неповторяющиеся записи (например хотим узнать какой вообще пол есть в таблице или из каких стран есть сотрудники, если добавить столбец со страной).  

**WHERE** - логический оператор "Где", условие для выборки по конкретному значению.  
`SELECT * FROM employee WHERE gender = 'Female';` - выведем только женщин; 
**AND**   
`SELECT * FROM employee WHERE gender = 'Female' AND first_name = 'Hanna';` - выведем женщин с именем Hanna;  
**OR**  
`SELECT * FROM employee WHERE gender = 'Female' AND (first_name = 'Hanna' OR first_name = 'Reta');` - женщины с именем Hanna и с именем Reta.  
**LIMIT** - ограничить выборку количеством записей в табл
`SELECT * FROM employee LIMIT 5;` - выведем 5 первых строк в таблице.  
**OFFSET** - с какой позиции искать.
`SELECT * FROM employee OFFSET 10 LIMIT 5;` - выведем 5 строк начиная с 10 позиции в таблице

![](/PostgreeSQL/screen/17_select_from.jpg)

**FETCH** - аналог **LIMIT**  
`SELECT * FROM employee OFFSET 10 FETCH FIRST 5 ROW ONLY;` - также выведем 5 строк начиная с 10 позиции в таблице.  

**IN** - перечислить несколько параметров для вывода  
`SELECT * FROM employee WHERE first_name IN ('Nilson', 'Shara', 'Fulvia');` - вывели строки, где встречаются указанные имена.  

**BETWEEN** - выбор промежутка (интервала/диапазона)  
`SELECT * FROM employee WHERE date_of_birthd BETWEEN '2022-01-01' AND '2022-12-12';` - вывели сотрудников, у кого ДР попадает в диапазон '2022-01-01' AND '2022-12-12'  

**LIKE** - поиск  
`SELECT * FROM employee WHERE email LIKE '%.com';` - вывели все адреса почтовых ящиков с доменом *com*.  
Чтобы не учитывался регистр (заглавные буквы) перед LIKE добавляем i = **iLIKE**  

**COUNT** - подсчет количества повторений  
`SELECT gender, COUNT(*) FROM employee GROUP BY gender;` - вывели количество, по сколько сотрудников каждого пола  

![](/PostgreeSQL/screen/18_select_COUNT.jpg)  

**HAVING** - условие (имеют)  
`SELECT gender, COUNT(*) FROM employee GROUP BY gender HAVING COUNT(*) > 20;` - вывели пол сотрудников, количество которых встречается больше 20 раз  

![](/PostgreeSQL/screen/19_select_COUNT_HAVING.jpg) 

**AS** - присвоить выводимым параметрам свои произвольные имена (например, для удобтства представления)  
`SELECT id, first_name AS name, last_name AS surname, date_of_birthd AS birthday FROM employee;` - вывели заголовки столбцов в более читабельном виде  

![](/PostgreeSQL/screen/20_select_AS.jpg) 

**COALESCE** - заполнить пустые значения  
`SELECT COALESCE(email, 'not applicable') FROM employee;` - вывели список email и заполнили пустые строки значением *not applicable*  

![](/PostgreeSQL/screen/21_select_COAL.jpg)

### V. Базовая Арифметика и Агрегаты  

1. Создадим новую таблицу - **holiday** (предположим, что работадатель оплачивает поездку в отпуск своим сотрудникам и ему нужно вести записи по таким событиям) 
В *mockaroo* создадим следующие поля (см. скрин)  

![](/PostgreeSQL/screen/22_mockaroo_holiday.jpg)

2. Приведем запрос к следующему виду

![](/PostgreeSQL/screen/22_mockaroo_holiday2.jpg)

3. Импортируем в БД  

![](/PostgreeSQL/screen/23_import_holiday.jpg)

**MAX()** - вывести максимальное значение  
**MIN()** - вывести минимальное значение 
**AVG** - среднее значение 

`SELECT MAX(price) FROM holiday;` - вывели максимальную стоимость путевки  

`SELECT MIN(price) FROM holiday;` - вывели минимальную стоимость путевки  

`SELECT AVG(price) FROM holiday;` - вывели среднюю стоимость путевки

**ROUND** - округлить до целых  

`SELECT ROUND(AVG(price)) FROM holiday;` - вывели среднее и округлили число до целых  

Решили вывести самые дорогие направления, чтобы не давать туда путевки сотрудникам:  

`SELECT distination_country, destination_city, MAX(price) FROM holiday GROUP BY distination_country, destination_city;`