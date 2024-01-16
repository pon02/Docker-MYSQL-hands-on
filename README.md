# Docker-MySQL-hands-on
## コンテナ起動・確認  
- コンテナ起動
```sh
makiba@PonBook docker-mysql-hands-on % docker compose up -d
[+] Building 30.7s (10/10) FINISHED                        docker:desktop-linux
 ✔ Network docker-mysql-hands-on_default  Created                          0.0s 
 ✔ Volume "docker-mysql-hands-on_my-vol"  Created                          0.0s 
 ✔ Container docker-mysql-hands-on        Started                          0.0s
```
- コンテナ確認
```sh
makiba@PonBook docker-mysql-hands-on % docker ps
CONTAINER ID   IMAGE                      COMMAND                   CREATED          STATUS          PORTS                               NAMES
b4ce78744e55   docker-mysql-hands-on-db   "docker-entrypoint.s…"   45 seconds ago   Up 40 seconds
33060/tcp, 0.0.0.0:3307->3306/tcp   docker-mysql-hands-on
```

## MySQLにログイン  
- ログイン
```sh
makiba@PonBook docker-mysql-hands-on % docker compose exec db mysql -uroot -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.35 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

## Movie_list確認・利用  
- Movie_list確認
```sh
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| movie_list         |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.09 sec)
```

- Movie_list利用開始
```sh
mysql> use movie_list;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```
- moviesテーブル確認
```sh
mysql> show tables;
+----------------------+
| Tables_in_movie_list |
+----------------------+
| movies               |
+----------------------+
1 row in set (0.03 sec)
```
- moviesテーブルのレコード確認
```sh
mysql> > select * from movies;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '> select * from movies' at line 1
mysql> select * from movies;
+----+--------------------------------+-----------------------------+
| id | name                           | director                    |
+----+--------------------------------+-----------------------------+
|  1 | ショーシャンクの空に           | フランク・ダラボン          |
|  2 | この世界の片隅に               | 片渕須直                    |
+----+--------------------------------+-----------------------------+
2 rows in set (0.01 sec)
```
- moviesテーブルにレコード追加
```sh
mysql> insert into movies (name, director) values ("トイレット", " 萩上直子");
Query OK, 1 row affected (0.05 sec)
```
- レコードの登録結果を確認
```sh
mysql> select * from movies;
+----+--------------------------------+-----------------------------+
| id | name                           | director                    |
+----+--------------------------------+-----------------------------+
|  1 | ショーシャンクの空に           | フランク・ダラボン          |
|  2 | この世界の片隅に               | 片渕須直                    |
|  3 | トイレット                     | 萩上直子                    |
+----+--------------------------------+-----------------------------+
3 rows in set (0.00 sec)
```
## MySQLログアウト
- ログアウト
```sh
mysql> exit
Bye
```

## Dockerコンテナの停止・確認
- Dockerの停止
```sh
makiba@PonBook docker-mysql-hands-on % docker compose down
[+] Running 2/2
 ✔ Container docker-mysql-hands-on        Removed                          0.9s 
 ✔ Network docker-mysql-hands-on_default  Removed                          0.0s
```
- 停止の確認
```sh
makiba@PonBook docker-mysql-hands-on % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

# 所感
作業はスムーズにできて、MySQLでDB内のレコードを編集できるということは理解できました。  
しかしDockerについてはまだ自分の理解が追いついておらず、"MySQLを使うための部屋"という認識なのですが、あっているのでしょうか。  
ハンズオンをやるたびに同じところに辿り着いている気がしますが、Dockerについても使いながら意味を探っていくようになりそうです。


