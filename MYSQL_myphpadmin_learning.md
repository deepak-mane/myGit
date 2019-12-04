# MySQL phpMyAdmin Learnings


### [ 1. ] error while loging into myphpadmin console
```
Mysql. The server requested authentication method unknown to the client [caching_sha2_password] #1390
```
<b>Solution<\b>
1. From bin directory in MySQLServer run 
```mysqld --init-file=E:\\INSTALL\\MySQLinstall\\mysql-init.txt --datadir=D:\\APP\\MySQL\\MySQLServerData\\Data```
2. Open MySQL 8.0 Command Line Client
3. Enter root password
4. Run command ```mysql> alter user 'root'@'localhost' identified with mysql_native_password by 'password' ```
