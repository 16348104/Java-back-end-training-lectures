# Install MySQL on MAC Yosemite 10.10.2

1. download mysql

    > [mysql-5.6.27-osx10.9-x86_64.tar.gz](http://mirrors.sohu.com/mysql/MySQL-5.6/mysql-5.6.27-osx10.9-x86_64.tar.gz)
    
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

2. cp /usr/local/mysql/my.cnf /ect/my.cnf

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
  | character_set_client     | utf8mb4            |
  | character_set_connection | utf8mb4            |
  | character_set_database   | utf8mb4            |
  | character_set_filesystem | binary             |
  | character_set_results    | utf8mb4            |
  | character_set_server     | utf8mb4            |
  | character_set_system     | utf8               |
  | collation_connection     | utf8mb4_unicode_ci |
  | collation_database       | utf8mb4_unicode_ci |
  | collation_server         | utf8mb4_unicode_ci |
  +--------------------------+--------------------+
  ```

4. mysql_connector version 5.1.13+

6. jdbc.properties

  ```
  jdbc.url=jdbc:mysql://127.0.0.1:3306/database?useUnicode=true&characterEncoding=utf8&autoReconnect=true&rewriteBatchedStatements=TRUE
  ```