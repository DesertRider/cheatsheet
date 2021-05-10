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

Dump d'une BD::

   mysqldump db-name > backup.sql
   mysqldump --no-data db-name > schema.sql
   
Dump d'une table d'une BD::

   mysqldump db-name table
   
Restore d'une BD::

   mysql -u root -p my_database < backup.sql

Exécution d'une requête sql directement via le command line::

   mysql -u root -p prod_int < demande1.sql  > resultat1.txt

Quelques commandes SQL
----------------------

Lister les BD::

   show databases;
   
Lister les tables d'une BD::

   use my_db;
   show tables;
   
Voir la structure d'une table::

   describe my_table;

Détruire une ligne::

   remove from users where username like 'xxx';
   
Mettre à jour plusieurs colonnes de plusieurs lignes::

   update users
      set oauth2_user_id = users.username,
          disable_login_form = 1,
          timezone = NULL,
          language = NULL
      where username like 'shqsrc';

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
