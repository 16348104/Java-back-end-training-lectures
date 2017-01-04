# Chapter 2 数据库安装 / 设置

> MySQL (mysql-5.6.30-win32.zip)

1. upzip zip file to your_mysql_directory/

2. Edit configuration file
	
    > your_mysql_directory/my.ini (rename my-default.ini to my.ini )

  ```
  [client]
  default-character-set=utf8

  [mysql]
  default-character-set=utf8

  [mysqld]
  collation-server = utf8_unicode_ci
  init-connect='SET NAMES utf8'
  character-set-server = utf8
  default-storage-engine = innodb
  ```

3. Install
	
    > cmd `your_mysql_directory/bin`

  ```dos
  C:\>d:
  D:\>cd your_mysql_directory/bin
  ```
  
  ```sql
  mysqld --install your_mysql_service_name --defaults-file=your_mysql_directory\my.ini

  (if your_mysql_directory include spaces,use double quotation marks)
  ```

4. Start / stop MySQL

  ```
  run > services.msc

  or:

  cmd
  net start your_mysql_service_name
  net stop your_mysql_service_name
  ```

5. Update MySQL password

  > cmd `your_mysql_directory/bin`
    
  ```sql
  mysql -u root -p

  update mysql.user set password = PASSWORD('your_new_password') where user='root';
  flush privileges;
  
  -- forgot root password
  # cmd1
  > mysqld -u root --skip-grant-tables
  # cmd2
  > mysql
  [ENTER]
  # update root password...
  ```
	
6. Check configuration
  
  ```sql    
  mysql> show variables like 'char%';
  mysql> show variables like 'coll%';
  ```

7. Delete service

  ```
  SC delete your_mysql_service_name
  ```

7. dump data
     
  > cmd `your_mysql_directory/bin`

  ```sql
  mysqldump -u root -p database > your_dump_file_name.sql

  ```
    
8. import data

  ```sql
  mysql> source your_dump_file_name.sql
  ```
  
> MySQL tar.gz install in MAC yosemite 10.10.2

1. download mysql

    - [mysql-5.6.27-osx10.9-x86_64.tar.gz](http://mirrors.sohu.com/mysql/MySQL-5.6/mysql-5.6.27-osx10.9-x86_64.tar.gz)
    
2. cd /Users/<YourName>/Downloads

3. tar zxvf mysql-5.6.24-osx10.9-x86_64.tar.gz

4. sudo mv mysql-5.6.24-osx10.9-x86_64 /usr/local/mysql

5. cd /usr/local

6. sudo chown -R root:wheel mysql

7. cd /usr/local/mysql

8. sudo scripts/mysql_install_db --user=mysql

9. cd /usr/local/mysql

## start / stop / restart / status

> sudo support-files/mysql.server start

> sudo support-files/mysql.server restart

> sudo support-files/mysql.server stop

> sudo support-files/mysql.server status

## mysql environment variable set

1. vi ~/.bash_profile

2. export PATH=${PATH}:/usr/local/mysql/bin

3. source ~/.bash_profile

4. echo $PATH

## utf8mb4 character

1. mysql 5.5.3+

2. alter

```sql
ALTER DATABASE database_name CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;
ALTER TABLE table_name CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
ALTER TABLE table_name CHANGE column_name column_name VARCHAR(191) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

2. sudo cp /usr/local/mysql/my.cnf /etc/my.cnf

```
[client]
default-character-set = utf8mb4

[mysql]
default-character-set = utf8mb4

[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
init_connect='SET NAMES utf8mb4'
```

3. check

```sql
SHOW VARIABLES WHERE Variable_name LIKE 'character_set_%' OR Variable_name LIKE 'collation%';
``` 

```
+--------------------------+--------------------+
| Variable_name            | Value              |
+--------------------------+--------------------+
| character_set_client    | utf8mb4            |
| character_set_connection | utf8mb4            |
| character_set_database  | utf8mb4            |
| character_set_filesystem | binary            |
| character_set_results    | utf8mb4            |
| character_set_server    | utf8mb4            |
| character_set_system    | utf8              |
| collation_connection    | utf8mb4_unicode_ci |
| collation_database      | utf8mb4_unicode_ci |
| collation_server        | utf8mb4_unicode_ci |
+--------------------------+--------------------+
```

4. mysql_connector version 5.1.13+

6. jdbc.properties

```
jdbc.url=jdbc:mysql://127.0.0.1:3306/database?useUnicode=true&characterEncoding=utf8&autoReconnect=true&rewriteBatchedStatements=TRUE
```
