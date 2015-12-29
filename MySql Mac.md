##MySql Mac

 
tomcat path:  

/var/lib/tomcat7  

sudo service tomcat7 restart  
sudo service tomcat7 stop  

Watch the tomcat console:  
sudo tail -f /var/log/tomcat7/catalina.out  


Backup your DB:  
mysqldump -u username -p password databaseName > backFileName.sql



http://www.macupdate.com/app/mac/6915/mysql/download


##How to install the MySQL into MAC computer:

https://www3.ntu.edu.sg/home/ehchua/programming/sql/MySQL_HowTo.html


	For Mac OS X
	Download the MySQL "DMG Archive" from http://dev.mysql.com/downloads/mysql/:
	Choose "General Available (GA) Releases" tab.
	In "Select Platform", choose the "Mac OS X".
	Select the appropriate "DMG Archive" for your specific Mac OS version:
	Click the Apple logo ⇒ "About this Mac" to check your Mac OS version.
	Read http://support.apple.com/kb/ht3696 to check if your Mac OS is 32-bit or 64-bit.
	For example, for Lion (10.7) and Core i7 processor, choose "Mac OS X ver. 10.7 (x86, 64-bit), DMG Archive (117.5M)".
	There is NO need to "Sign-up" - Just click "No thanks, just start my download".
	To install MySQL:
	Go to "Downloads" ⇒ Double-click ".dmg" file downloaded.
	Double-click the "mysql-5.6.{xx}-osx10.x-xxx.pkg" ⇒ Follow the instructions to install MySQL. Click "continue" if "unindentified developer" warning dialog appears. (If double-click has no response, right-click ⇒ open with ⇒ installer.)
	MySQL will be installed in "/usr/local/mysql-5.6.{xx}-osx10.x-x86_xx" directory. A symbolic link "/usr/local/mysql" will be created automatically to the MySQL installed directory.
	Eject the ".dmg" file.
	(For MySQL 5.7) [TODO] Check if initialization needed?!
	MySQL will be installed in /usr/local/mysql. Take note of this installed directory!!
 

##how to shutdown:

To shutdown the server, start a new Terminal and issue:
Prompt$ cd /usr/local/mysql/bin
 
Prompt$ sudo ./mysqladmin -u root -p shutdown
      // Hit "Enter" key when you are prompted for the password


##how to start to use it:
 
Open a new "Terminal" and issue these commands to start a MySQL client with superuser root:
-- Change the current directory to <MYSQL_HOME>\bin.
Prompt$ cd /usr/local/mysql/bin
 
-- Start a client with superuser "root"
Prompt$ ./mysql -u root -p
Enter password:     // Hit "Enter" key for empty password set in installation 
Welcome to the MySQL monitor.  Commands end with ; or \g.
......
-- Client started. The prompt changes to "mysql>".
-- You can now issue SQL commands.
mysql>






##cannot connect to MySQL:

Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
 
 
sudo /usr/local/mysql/support-files/mysql.server start 



##change password of mysql:

 MySQL 5.7.6 and later:

ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass';

MySQL 5.7.5 and earlier:

SET PASSWORD FOR 'root'@'localhost' = PASSWORD('MyNewPass');



## create DB:

create database if not exists studentdb;

show databases;








	-- Start a client, if it is not started
	-- cd to the MySQL's bin directory
	> mysql -u myuser -p     // Windows
	$ ./mysql -u myuser -p   // Mac OS X
	   
	-- Create a new database called "studentdb"
	mysql> create database if not exists studentdb;
	Query OK, 1 row affected (0.08 sec)
	   
	-- list all the databases in this server
	mysql> show databases;
	+--------------------+
	| Database           |
	+--------------------+
	| information_schema |
	| mysql              |
	| performance_schema |
	| studentdb          |
	| test               |
	+--------------------+
	5 rows in set (0.07 sec)
	   
	-- Use "studentdb" database as the default database
	-- You can refer to tables in the default database by tablename alone, instead of databasename.tablename
	mysql> use studentdb;
	Database changed
	   
	-- Remove the table "class101" in the default database if it exists
	mysql> drop table if exists class101;
	Query OK, 0 rows affected (0.15 sec)
	   
	-- Create a new table called "class101" in the default database 
	--  with 3 columns of the specified types
	mysql> create table class101 (id int, name varchar(50), gpa float);
	Query OK, 0 rows affected (0.15 sec)
	   
	-- List all the tables in the default database "studentdb"
	mysql> show tables;
	+---------------------+
	| Tables_in_studentdb |
	+---------------------+
	| class101            |
	+---------------------+
	1 row in set (0.00 sec)
	   
	-- Describe the "class101" table (list its columns' definitions)
	mysql> describe class101;
	+-------+-------------+------+-----+---------+-------+
	| Field | Type        | Null | Key | Default | Extra |
	+-------+-------------+------+-----+---------+-------+
	| id    | int(11)     | YES  |     | NULL    |       |
	| name  | varchar(50) | YES  |     | NULL    |       |
	| gpa   | float       | YES  |     | NULL    |       |
	+-------+-------------+------+-----+---------+-------+
	3 rows in set (0.04 sec)
	   
	-- Insert a row into "class101" table.
	-- Strings are to be single-quoted. No quotes for INT and FLOAT.
	mysql> insert into class101 values (11, 'Tan Ah Teck', 4.8);
	Query OK, 1 row affected (0.03 sec)
	   
	-- Insert another row
	mysql> insert into class101 values (22, 'Mohamed Ali', 4.9);
	Query OK, 1 row affected (0.03 sec)
	   
	-- Select all columns (*) from table "class101"
	mysql> select * from class101;
	+----+-------------+------+
	| id | name        | gpa  |
	+----+-------------+------+
	| 11 | Tan Ah Teck |  4.8 |
	| 22 | Mohamed Ali |  4.9 |
	+----+-------------+------+
	2 rows in set (0.00 sec)
	  
	-- Select columns from table "class101" with criteria
	mysql> select name, gpa from class101 where gpa > 4.85;
	+-------------+------+
	| name        | gpa  |
	+-------------+------+
	| Mohamed Ali |  4.9 |
	+-------------+------+
	1 rows in set (0.00 sec)
	  
	-- Update selected records
	mysql> update class101 set gpa = 4.4 where name = 'Tan Ah Teck';
	Query OK, 1 row affected (0.03 sec)
	   
	mysql> select * from class101;
	+----+-------------+------+
	| id | name        | gpa  |
	+----+-------------+------+
	| 11 | Tan Ah Teck |  4.4 |
	| 22 | Mohamed Ali |  4.9 |
	+----+-------------+------+
	2 rows in set (0.00 sec)
	 
	-- delete selected records
	mysql> delete from class101 where id = 22;
	Query OK, 1 row affected (0.03 sec)
	   
	mysql> select * from class101;
	+----+-------------+------+
	| id | name        | gpa  |
	+----+-------------+------+
	| 11 | Tan Ah Teck |  4.4 |
	+----+-------------+------+
	1 rows in set (0.00 sec)
	 
	-- You can store SQL commands in a file (called SQL script) and run the script.
	-- Use a text editor to CREATE a NEW FILE called "mycommands.sql" 
	--   containing the following three SQL statements.
	-- (For Windows) Save the file under "d:\myProject".
	-- (For Mac OS X) Save the file under "Documents".
	insert into class101 values (33, 'Kumar', 4.8);
	insert into class101 values (44, 'Kevin', 4.6);
	Select * from class101;

	-- Once you have created the file, you can use the following "source" command 
	--   to run the SQL script.
	-- You need to provide the full path to the script.
	-- (For Windows) The filename is d:\myProject\mycommands.sql.
	-- (For Mac OS X) The filename is ~/Documents/mycommands.sql
	mysql> source d:\myProject\mycommands.sql   // For Windows
	mysql> source ~/Documents/mycommands.sql    // For Mac OS X
	Query OK, 1 row affected (0.00 sec)   -- INSERT command output
	Query OK, 1 row affected (0.00 sec)   -- INSERT command output
	+------+-------------+------+         -- SELECT command output
	| id   | name        | gpa  |
	+------+-------------+------+
	|   11 | Tan Ah Teck |  4.4 |
	|   33 | Kumar       |  4.8 |
	|   44 | Kevin       |  4.6 |
	+------+-------------+------+
	3 rows in set (0.00 sec)

