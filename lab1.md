# **Лабораторная работа №1**
_Выполнила: Пацан Мария 2ПОО_
## **Задание 1** 
### Раздел "Management"
1. Раздел "Server Status". В разделе отображается общая информация о сервере и подключении к нему. Информация логически сгруппирована. Можно выделить следующие группы: a. Общая информация (например, название хоста, номер порта, версия БД). b. Настройки сервера (например, включен ли брандмауэр, используется ли SSL) c. Каталоги сервера d. Сводка по используемым ресурсам компьютера (ОЗУ, процессор и т. д.) e. Настройки соединения SSL (если SSL включена).
2. Раздел "Client Connections". В разделе отображается список активных и «спящих» клиентских подключений к серверу MySQL. Для каждого подключения доступна детальная информация, сгруппированная по вкладкам: a. Details — идентификатор процесса (Process ID), тип, пользователь, хост и другие сведения о соединении. b. Locks — информация о блокировках метаданных (MDL), включая заблокированные подключения и ожидающие их запросы (требует MySQL 5.7.3+). c. Attributes — атрибуты подключения, такие как операционная система, имя и версия клиента, платформа. Также доступна возможность принудительно завершить конкретный запрос или соединение.
3. Раздел "Users and Privileges". В разделе реализовано управление учётными записями пользователей MySQL и их правами доступа. Доступны следующие задачи: a. Создание, изменение и удаление учётных записей. b. Настройка аутентификации (тип плагина, пароль, ограничение по хостам). c. Установка лимитов на количество запросов, обновлений и одновременных подключений в час. d. Назначение административных ролей (DBA, MaintenanceAdmin, UserAdmin и др.). e. Тонкая настройка привилегий на уровне отдельных схем (Schema Privileges).
4.Раздел "Status and System Variables". В разделе отображается полный список серверных переменных (статусных и системных) для активного подключения. Информация представлена в виде таблицы с именем переменной, её значением (если применимо) и описанием. Список можно фильтровать по имени или по категории (например, InnoDB). Начиная с MySQL Workbench 8.0.11, доступна функция «Persist» — сохранение выбранных глобальных переменных для их применения после перезапуска сервера.
5. Раздел "Data Export". В разделе реализован мастер экспорта данных MySQL. Можно выбрать схемы и отдельные объекты (таблицы) для экспорта, а также настроить параметры: экспорт в проектную папку или в один SQL-файл, включение хранимых процедур и событий, пропуск данных таблиц. Для выполнения операций используется утилита mysqldump.
6. Раздел "Data Import/Restore". В разделе представлен мастер импорта ранее экспортированных данных (из проектной папки или SQL-файла). Можно выбрать схему для импорта или создать новую, а также отслеживать прогресс операции на вкладке «Import Progress».
### Раздел "Instance" ("Экземпляр БД")
1. Раздел "Startup / Shutdown". В разделе реализованы функции запуска и остановки сервера MySQL. Доступны кнопки «Startup» и «Shutdown», а также просмотр журнала запуска (Startup Message Log) и текущего статуса экземпляра.
2. Раздел "Server Logs". В разделе отображаются журналы сервера MySQL. По умолчанию доступен журнал ошибок (Error Log). При включении соответствующих настроек становятся доступны журналы медленных запросов (Slow Query Log) и общих запросов (General Query Log).
3. Раздел "Options File". В разделе представлен графический редактор конфигурационного файла MySQL (например, my.cnf или my.ini). Изменения, внесённые в этом разделе, сохраняются в файле настроек после нажатия кнопки «Apply», однако для их применения может потребоваться перезапуск сервера.
### Раздел "Performance" ("Производительность")
1. Раздел "Dashboard". В разделе отображается графическая сводка ключевых показателей производительности сервера в реальном времени. Информация логически сгруппирована. Можно выделить следующие группы: a. Network Status — состояние сети: объём переданных/полученных данных и количество клиентских подключений. b. MySQL Status — состояние MySQL: эффективность кэша открытых таблиц, количество выполненных SQL-запросов и счётчики (в секунду) для SELECT, INSERT, UPDATE, DELETE, CREATE, ALTER, DROP. c. InnoDB Status — состояние InnoDB: использование буферного пула, дисковый ввод-вывод (redo log, doublewrite buffer), чтение и запись данных.
2. Раздел "Performance Reports". В разделе представлены готовые отчёты на основе данных Performance Schema (через представления схемы sys). Отчёты позволяют анализировать узкие места ввода-вывода, выявлять ресурсоёмкие SQL-запросы, отслеживать использование временных таблиц, полные сканирования таблиц и ошибки/предупреждения.
3. Раздел "Performance Schema Setup". В разделе реализована графическая настройка инструментов Performance Schema. Начальная вкладка «Easy Setup» позволяет включить или отключить сбор статистики одним переключателем. Дополнительные настройки (Show Advanced) дают доступ к детальной конфигурации отдельных инструментов (instruments) и таймеров.

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
('Sasha',  ‘sasha@gmail.com');

UPDATE `simpledb`.`users` SET `email` = 'oleg@hotmail.ru' WHERE (`id` = ‘2'); 
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

Будет ли возможно добавить резюме с несуществующим userid? Каков результат? Почему так происходит? Нет, вставка невозможна. MySQL выдаёт ошибку ERROR 1452: «Cannot add or update a child row: a foreign key constraint fails». СУБД отказывается вставлять строку, потому что resume.userid ссылается на несуществующую запись в users.id.
Внешний ключ resume_users обеспечивает ссылочную целостность: в дочерней таблице не может быть ссылок на несуществующих родителей. Это защищает базу от одиночных записей - резюме, которое ни к какому пользователю не привязано.

## **Задание 10**
``` sql
DELETE FROM `simpledb`.`users` WHERE (`id` = '3');
```

При удалении пользователя Sofia (id = 3) сработала настройка ON DELETE CASCADE. MySQL автоматически удалил не только саму запись из таблицы users, но и все связанное с ней резюме из таблицы resume.

``` sql
UPDATE `simpledb`.`users` SET `id` = '100' WHERE (`id` = '1'); 
```
При изменении id пользователя Maria с 1 на 100 сработала настройка ON UPDATE CASCADE. В таблице resume поле userid автоматически обновилось с 3 на 100. Связь между пользователем и его резюме сохранилась, вручную обновлять userid не  потребовалось.

![2](https://i.ibb.co/jPhTmp9M/2026-09-12-21-21-40.png)
