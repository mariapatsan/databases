# **Лабораторная работа №1**
_Выполнила: Пацан Мария 2ПОО_
## **Задание 1** 
### Раздел "Management"
1. Server Status - общая информация о сервере и подключении: хост, порт, версия БД, настройки SSL, каталоги, ресурсы (ОЗУ, процессор).
2. Client Connections - список активных и «спящих» подключений. Вкладки: Details (Process ID, пользователь, хост), Locks (блокировки метаданных, MySQL 5.7.3+), Attributes (ОС, клиент, платформа). Можно принудительно завершить запрос или соединение.
3. Users and Privileges - управление учётными записями и правами: создание/изменение/удаление, аутентификация (плагин, пароль, хост), лимиты запросов и подключений в час, административные роли (DBA и др.), привилегии на уровне схем.
4. Status and System Variables - таблица серверных переменных (имя, значение, описание) с фильтрацией по имени и категории. С Workbench 8.0.11 есть Persist - сохранение глобальных переменных после перезапуска.
5. Data Export - мастер экспорта: выбор схем и таблиц, экспорт в папку или один SQL-файл, включение процедур/событий, пропуск данных. Использует mysqldump.
6. Data Import/Restore - мастер импорта из папки или SQL-файла: выбор/создание схемы, прогресс на вкладке Import Progress.
   
### Раздел "Instance" ("Экземпляр БД")
1. Startup / Shutdown - запуск и остановка сервера: кнопки «Startup»/«Shutdown», журнал запуска, статус экземпляра.
2. Server Logs - журналы сервера: по умолчанию Error Log; при включении - Slow Query Log и General Query Log.
3. Options File - редактор конфигурации (my.cnf / my.ini). Сохранение по «Apply», для применения нужен перезапуск.
   
### Раздел "Performance" ("Производительность")
1. Dashboard - сводка в реальном времени: Network Status (трафик, подключения), MySQL Status (кэш таблиц, запросы и счётчики в секунду для SELECT/INSERT/UPDATE/DELETE/CREATE/ALTER/DROP), InnoDB Status (буферный пул, дисковый ввод-вывод).
2. Performance Reports - готовые отчёты на базе Performance Schema (схема sys): узкие места ввода-вывода, ресурсоёмкие запросы, временные таблицы, полные сканирования, ошибки/предупреждения.
3. Performance Schema Setup - настройка инструментов Performance Schema: Easy Setup (вкл/выкл одним переключателем), Show Advanced (детальная конфигурация instruments и таймеров).

## **Задание 3** 
``` sql
CREATE TABLE `users` (
  `id` int NOT NULL AUTO_INCREMENT,
  `name` varchar(45) NOT NULL,
  `email` varchar(45) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email_UNIQUE` (`email`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3; 
```

## **Задание 4** 
``` sql
INSERT INTO `simpledb`.`users` (`name`, `email`) VALUES
('Maria',  'maria@mail.ru'),
('Oleg',   'oleg@hotmail.ru'),
('Sofia',  'sofa@mail.ru'),
('George', 'george@gmail.com'),
('Sasha',  'sasha@gmail.com');

UPDATE `simpledb`.`users` SET `email` = 'oleg@hotmail.ru' WHERE (`id` = '2'); 
```

## **Задание 5** 
Поле created имеет тип TIMESTAMP и значение по умолчанию CURRENT_TIMESTAMP(). Это означает, что при вставке новой строки без указания значения для этого поля MySQL автоматически подставит текущие дату и время сервера. Такое поле удобно использовать как «дату создания записи». Значение можно переопределить, указав его явно в INSERT. При обычном DEFAULT CURRENT_TIMESTAMP() значение поля не меняется при последующих обновлениях строки.
Обязательными (NOT NULL) оставлены только id (первичный ключ, заполняется автоматически) и created (служебное поле с DEFAULT CURRENT_TIMESTAMP(), тоже заполняется автоматически).
Это позволяет регистрировать пользователя, не требуя от него личных данных, но при этом сохраняет целостность базы: каждая строка имеет уникальный идентификатор и дату создания.

``` SQL
ALTER TABLE `simpledb`.`users` 
ADD COLUMN `gender` ENUM('M', 'F') NULL AFTER `email`,
ADD COLUMN `bday` DATE NULL AFTER `gender`,
ADD COLUMN `postal_code` VARCHAR(10) NULL AFTER `bday`,
ADD COLUMN `rating` FLOAT NULL AFTER `postal_code`,
ADD COLUMN `created` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP() AFTER `rating`,
CHANGE COLUMN `name` `name` VARCHAR(50) NULL ,
CHANGE COLUMN `email` `email` VARCHAR(45) NULL ;
```

![1](https://i.ibb.co/wZz3bvCx/2026-09-12-21-21-18.png)

## **Задание 6** 
С помощью внесения данных вручную:
``` SQL
UPDATE `simpledb`.`users` SET `gender` = 'F', `bday` = '1999-03-15', `postal_code` = '10100', `rating` = '4.8' WHERE (`id` = '1');
UPDATE `simpledb`.`users` SET `gender` = 'M', `bday` = '1997-07-22', `postal_code` = '12345', `rating` = '3.7' WHERE (`id` = '2');
UPDATE `simpledb`.`users` SET `gender` = 'F', `bday` = '2001-11-02', `postal_code` = '54321', `rating` = '4.9' WHERE (`id` = '3');
```
 
С помощью выполнения SQL-запросов :
``` SQL
UPDATE `simpledb`.`users` 
SET `gender`='M', `bday`='1995-05-30', `postal_code`='190000', `rating`=4.2 
WHERE `id`=4;
UPDATE `simpledb`.`users` 
SET `gender`='F', `bday`='2000-09-18', `postal_code`='630000', `rating`=4.5 
WHERE `id`=5;
```

## **Задание 7** 
``` SQL
/*
-- Query: SELECT * FROM simpledb.users
LIMIT 0, 1000

-- Date: 2026-09-12 19:20
*/
INSERT INTO `` (`id`,`name`,`email`,`gender`,`bday`,`postal_code`,`rating`,`created`) VALUES (1,'Maria','maria@mail.ru','F','1999-03-15','10100',4.8,'2026-09-12 16:05:50');
INSERT INTO `` (`id`,`name`,`email`,`gender`,`bday`,`postal_code`,`rating`,`created`) VALUES (2,'Oleg','oleg@hotmail.ru','M','1997-07-22','12345',3.7,'2026-09-12 16:05:50');
INSERT INTO `` (`id`,`name`,`email`,`gender`,`bday`,`postal_code`,`rating`,`created`) VALUES (3,'Sofia','sofa@mail.ru','F','2001-11-02','54321',4.9,'2026-09-12 16:05:50');
INSERT INTO `` (`id`,`name`,`email`,`gender`,`bday`,`postal_code`,`rating`,`created`) VALUES (4,'George','george@gmail.com','M','1995-05-30','190000',4.2,'2026-09-12 16:05:50');
INSERT INTO `` (`id`,`name`,`email`,`gender`,`bday`,`postal_code`,`rating`,`created`) VALUES (5,'Sasha','sasha@gmail.com','F','2000-09-18','630000',4.5,'2026-09-12 16:05:50');
```

## **Задание 8**
``` SQL
CREATE TABLE `simpledb`.`resume` (
  `resumeid` INT NOT NULL AUTO_INCREMENT,
  `userid` INT NOT NULL,
  `title` VARCHAR(100) NOT NULL,
  `skills` TEXT NULL,
  `created` TIMESTAMP NULL DEFAULT CURRENT_TIMESTAMP(),
  PRIMARY KEY (`resumeid`));

ALTER TABLE `simpledb`.`resume` 
ADD INDEX `resume_users_idx` (`userid` ASC) VISIBLE;
;
ALTER TABLE `simpledb`.`resume` 
ADD CONSTRAINT `resume_users`
  FOREIGN KEY (`userid`)
  REFERENCES `simpledb`.`users` (`id`)
  ON DELETE CASCADE
  ON UPDATE CASCADE;
```

Внешний ключ resume_users связывает поле resume.userid с полем users.id. Выбраны действия ON DELETE CASCADE и ON UPDATE CASCADE.
При удалении пользователя из users - все связанные с ним резюме в resume автоматически удаляются.
При удалении резюме из resume - таблица users не затрагивается, так как каскад настроен только в одну сторону.
При изменении id пользователя в users - поле userid во всех его резюме автоматически обновляется на новое значение.
Внешний ключ не допускает ссылок на несуществующих пользователей.

## **Задание 9**
Максимум не ограничен - у одного пользователя может быть любое количество резюме. Ограничение - только физические ресурсы сервера (место на диске, размер таблицы).

Минимум 0 - пользователь может не иметь ни одного резюме. Это возможно, потому что внешний ключ resume.userid - users.id не требует, чтобы у каждого пользователя были резюме.

``` sql
/*
-- Query: SELECT * FROM simpledb.resume
LIMIT 0, 1000

-- Date: 2026-09-12 19:44
*/
INSERT INTO `` (`resumeid`,`userid`,`title`,`skills`,`created`) VALUES (1,1,'Team Lead','managment, Java, mentoring','2026-09-12 16:42:35');
INSERT INTO `` (`resumeid`,`userid`,`title`,`skills`,`created`) VALUES (2,3,'Data Analyst','SQL, Python','2026-09-12 16:42:35');


Error: There was an error while applying the SQL script to the database.
Operation failed: There was an error while applying the SQL script to the database.
Executing:
INSERT INTO `simpledb`.`resume` (`userid`, `title`, `skills`) VALUES ('10', 'Manager', 'HTML, communication');

ERROR 1452: 1452: Cannot add or update a child row: a foreign key constraint fails (`simpledb`.`resume`, CONSTRAINT `resume_users` FOREIGN KEY (`userid`) REFERENCES `users` (`id`) ON DELETE CASCADE ON UPDATE CASCADE)
SQL Statement:
INSERT INTO `simpledb`.`resume` (`userid`, `title`, `skills`) VALUES ('10', 'Manager', 'HTML, communication’)
```

Будет ли возможно добавить резюме с несуществующим userid? Каков результат? Почему так происходит? Нет, вставка невозможна. 
MySQL выдаёт ошибку ERROR 1452: «Cannot add or update a child row: a foreign key constraint fails». СУБД отказывается вставлять строку, потому что resume.userid ссылается на несуществующую запись в users.id.
Внешний ключ resume_users обеспечивает ссылочную целостность. Это защищает базу от одиночных записей.

## **Задание 10**
``` sql
DELETE FROM `simpledb`.`users` WHERE (`id` = '3');
```

При удалении пользователя Sofia (id = 3) сработала настройка ON DELETE CASCADE. MySQL автоматически удалил не только саму запись из таблицы users, но и все связанное с ней резюме из таблицы resume.

``` sql
UPDATE `simpledb`.`users` SET `id` = '100' WHERE (`id` = '1'); 
```
При изменении id пользователя Maria с 1 на 100 сработала настройка ON UPDATE CASCADE. В таблице resume поле userid автоматически обновилось с 1 на 100. Связь между пользователем и его резюме сохранилась, вручную обновлять userid не  потребовалось.

![2](https://i.ibb.co/jPhTmp9M/2026-09-12-21-21-40.png)
