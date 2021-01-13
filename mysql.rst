MySQL et MariaDB
================

Création, destruction, ...
--------------------------

Création d'une BD::

   CREATE DATABASE database_name;
   
Destruction d'une BD::

   DROP DATABASE [IF EXISTS] database_name;
   
Copie d'un BD mysql d'un serveur à un autre::

   mysqldump db-name | mysql -h remote.box.com db-name
   # Use ssh if you don't have direct access to remote mysql server (secure method):
   mysqldump db-name | ssh user@remote.box.com mysql db-name

Dump du schéma seulement::

   mysqldump --no-data db-name

Exécution d'une requête sql directement via le command line::

   mysql -u root -p prod_int < demande1.sql  > resultat1.txt

Quelques commandes SQL
----------------------

Size des databases MySql::

   SELECT table_schema "DB Name", 
      Round(Sum(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB" 
   FROM  information_schema.tables 
   GROUP  BY table_schema;

Quelques commandes MySQL / MariaDB ::

   select host,user from mysql.user;
   show databases;
   use nom_database;
   show tables;
   describe nom_table;
   delete from be_users where username='admin';

debug des commandes envoyées à Mysql::

   mkdir /var/log/mysql
   chown mysql:mysql /var/log/mysql
   mysql -u root -p
   SET GLOBAL general_log_file='/var/log/mysql/mariadb.log';
   (ce n'est pas permanent, un restart du serveur lui reset le nom du fichier)
   (sinon modifier mysql.cnf)
   SET GLOBAL log_output = 'FILE';
   SET GLOBAL general_log = 'ON';
   SHOW VARIABLES LIKE "general_log%";
   # Try to execute your own SQL query from your app or command-line tool...
   less /var/log/mysql/mariadb.log
   SET GLOBAL general_log = 'OFF';
   (ce n'est pas permanent)