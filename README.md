# Домашнее задание к занятию «Работа с данными (DDL/DML)»
*Асадбеков Асадбек*

## Задание 1

**1. Развёртывание MySQL 8 в Docker**

```bash
docker run --name mysql-8 -e MYSQL_ROOT_PASSWORD=root -d -p 3306:3306 mysql:8.0
```

**2. Создание пользователя `sys_temp`**

```sql
CREATE USER 'sys_temp'@'%' IDENTIFIED BY 'password';
```

**3. Получение списка пользователей (скриншот)**

```sql
SELECT user, host FROM mysql.user;
```

![alt text](https://github.com/asad-bekov/hw-12/blob/main/img/1.png)

**4. Выдача всех прав пользователю `sys_temp`**

```sql
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

**5. Проверка прав пользователя `sys_temp` (скриншот)**

```sql
SHOW GRANTS FOR 'sys_temp'@'%';
```

![alt text](https://github.com/asad-bekov/hw-12/blob/main/img/2.png)

**6. Подключение от имени `sys_temp`**

```bash
docker exec -it mysql-8 mysql -u sys_temp -p
```

**7. Загрузка базы `sakila`**

```bash
# Скачиваем дамп 
wget https://downloads.mysql.com/docs/sakila-db.zip

# Распаковываем
unzip sakila-db.zip

# Копируем файлы в контейнер
docker cp sakila-schema.sql mysql8:/sakila-schema.sql
docker cp sakila-data.sql mysql8:/sakila-data.sql

# Восстанавливаем базу
docker exec -it mysql8 mysql -u root -p < /sakila-schema.sql
docker exec -it mysql8 mysql -u root -p < /sakila-data.sql
```

**8. Просмотр всех таблиц в базе `sakila` (скриншот)**

```sql
SHOW TABLES;
```

![alt text](https://github.com/asad-bekov/hw-12/blob/main/img/3.png)

## Задание 2

**9. Таблица с первичными ключами (скриншот)**

![alt text](https://github.com/asad-bekov/hw-12/blob/main/img/4.png)

## Задание 3

**10. Ограничение прав пользователя `sys_temp`**

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'sys_temp'@'%';
GRANT SELECT ON sakila.* TO 'sys_temp'@'%';
FLUSH PRIVILEGES;
```

**11. Проверка ограниченных прав (скриншот)**

```sql
SHOW GRANTS FOR 'sys_temp'@'%';
```

![alt text](https://github.com/asad-bekov/hw-12/blob/main/img/5.png)

---