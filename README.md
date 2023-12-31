# Домашнее задание к занятию «Работа с данными (DDL/DML)» - `Бызгаев Александр`  
---

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.  
1.2. Создайте учётную запись sys_temp.   
1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)  
1.4. Дайте все права для пользователя sys_temp.   
1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)  
1.6. Переподключитесь к базе данных от имени sys_temp.  
Для смены типа аутентификации с sha2 используйте запрос:   
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.  
1.7. Восстановите дамп в базу данных.  
1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)  
*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*    

---  

### Решение  

1.1 Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker

В Debian и его производных, начиная с определенного момента, пакет mysql-server был заменен на mariadb-server в официальных репозиториях, так как MariaDB стал форком MySQL
и заменил его во многих дистрибутивах Linux из-за опасений, связанных с правами собственности на MySQL

```
установил и смотрим статус 
sudo systemctl status mysql.service

```
![image](https://github.com/Byzgaev-I/DDL-DML/blob/main/1.png)

1.2 Создайте учётную запись sys_temp

```
mysql -u root -p 
create user 'sys_temp'@'%' identified by '1234';
exit
```
1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

```
mysql -u root -p 
select User,Host from mysql.user;
exit
```
![image](https://github.com/Byzgaev-I/DDL-DML/blob/main/2.png)

1.4. Дайте все права для пользователя sys_temp

```
mysql -u root -p 
grant ALL PRIVILEGES on *.* to 'sys_temp'@'%' with GRANT option;
flush privileges;
exit
```
1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

```
mysql -u root -p 
show grants for 'sys_temp'@'%';
exit
```

![image](https://github.com/Byzgaev-I/DDL-DML/blob/main/4.png)

1.6. Переподключитесь к базе данных от имени sys_temp.
Для смены типа аутентификации с sha2 используйте запрос:
```
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
```
mysql -u sys_temp -p 
alter user 'sys_temp'@'%' IDENTIFIED with mysql_native_password by '1234';
exit
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

```
wget -c https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
cd sakila-db
```
1.7  Восстановите дамп в базу данных.

```
mysql -u sys_temp -p
show databases;
create database SakilaDB;
show databases;
use SakilaDB;
show tables;
source sakila-schema.sql;
source sakila-data.sql;
show tables;
exit
```

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

```
mysql -u sys_temp -p
show databases;
use SakilaDB;
show tables;
exit
```
![image](https://github.com/Byzgaev-I/DDL-DML/blob/main/6.png)

---
### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```

![image](https://github.com/Byzgaev-I/DDL-DML/blob/main/2-1.png)






