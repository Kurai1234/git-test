#Setting up Postgresql#

##Installation##
1. Sign into ubuntu server and type
```
sudo apt insttall postgresql
```

##Configuration##
1. To allow multiple TCP/IP connection. Config the 'postgresql.conf' file.
2. To access the directory of this file. Type:
```
cd /etc/postgresql/12/main
```
3.Then finally 'vim postgresql.conf' and look for the 'listen_addresses=' and change 'localhost' to '*'

##Connecting and creating a database##
1. Enter postgresql with the following command
```
sudo -u postgres psql
```
2. Type the following 2 commands to create a database and check the list of databases 
```
CREATE DATABASE <database name>;
\list
```

3.To connect to a database use the the '\c <database>' command, in my case the 'pink turtle' database
```
\c pinkturtle
```

-the following output will show that you are connected
```
You are now connected to database ''pinkturtle'' as user ''postgres''.
```
##Creating a new User##
1.to create a new user, use the 'CREATE USER' command.
```
CREATE USER pinkturtle WITH PASSWORD '123';
```
2. To exit postgresql, type the 'exit;' command and it will bring you back to 'home directory'.


##logging in a database with a new user##

1. execute the query
```
psql --host=localhost --dbname=<database name> --user=<user>
```
###Example###
```
psql --host=localhost --dbname=pinkturtle --user=pinkturtle
```

##Check current user on database##
1. To check how much users on the database, use the 'SELECT current_user'. 





#Nginx Web Server#
##Installation and Configuration##
1.Installing Nginx, type the following commands:
```
sudo apt update
sudo apt install nginx
```
2. To list all availabel applications, use the `ufw` command:
```
sudo ufw app list
```
-Output should show
```
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```

3.To allow connection, type the following command:
```
sudo ufw allow 'Nginx HTTP'
```
Verify the changes
```
sudo ufw status
```
-The output should show this.
```
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```
--If it says inactive type the following command
```
sudo ufw enable
```

4.Verify your everything is running, type the 'systemctl status nginx' and you should receive the followin.
```

Output
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2020-04-20 16:08:19 UTC; 3 days ago
     Docs: man:nginx(8)
 Main PID: 2369 (nginx)
    Tasks: 2 (limit: 1153)
   Memory: 3.5M
   CGroup: /system.slice/nginx.service
           ├─2369 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           └─2380 nginx: worker process
```


5. Finally to see if your server is running, go to your local machine and type the following command into your web browser.
```
http://<your server ip>
```
-to check your server ip address, type the 'ip a' command and use the ip listed after `inet`.
-usually its a ip after the 2:enp0s3 block.

6.Done correctly, the landing page would output 'Welcome to Nginx'
