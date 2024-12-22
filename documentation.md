 ## Client Server Architecture using MySQL
 
Step 1. Create and configure two linux-based virtual servers (EC2 instance in AWS)
![alt text](<launch instance.png>)
![alt text](2_ins_selectewd.png)

### On mysql server Linux Server install MySQL Server software.
ssh into an istance using the following:
``` sh
ssh -i proj3.pem ubuntu@13.61.6.100
```
![alt text](server_ssh.png)
``` sh
sudo apt update
```
![alt text](s_update.png)
``` sh
sudo apt upgrade
```
![alt text](s_upgrade.png)
``` sh
sudo apt install mysql-server
```
![alt text](install_mysql_server.png)
**I start the mysql service**
``` sh
sudo systemctl start mysql
```
**Check the Status**
``` sh
sudo systemctl status mysql
```
![alt text](server_status.png)
### On mysql client Linux Server install MySQL Client software.
**I copy the public Ip to ssh into the client _instance**
![](assets/2024-12-21-17-51-19.png)
``` sh
ssh -i proj3.pem ubuntu@13.49.73.183
```
![alt text](c_ssh.png)
**I update the Ubuntu**
``` sh
sudo apt update
```
![alt text](c_update.png)
**I upgrade the Ubuntu**
``` sh
sudo apt uprade
```
![alt text](c_upgrade.png)
**I install the Mysql-client**
``` sh
sudo apt install mysql-client
```
![](install_mysql_client.png)
**I move back to the server.**  
**I started the security strengthening**
``` sh
sudo mysql_secure_installation
```
![alt text](s_secure_install.png)
**I access mysql using the root privilege, I then proceed to creating a user**
``` sh
sudo mysql 
```
![](s_mysql_sudo_login.png)
**I created a USER**     
**I created a database**
``` sh
CREATE USER 'chuks'@'%' IDENTIFIED BY 'Pas$wd12'
CREATE DATABASE sercli
```
![](assets/2024-12-21-18-15-01.png)
**I logged into the just created user account the same server not mysql-client**
``` sh
mysql -u chuks -p
```
![](assets/2024-12-21-18-16-49.png)
**I grant the user some privilegs**
``` sh
GRANT SELECT, INSERT ON sercli.* TO 'chuks'@'%';
```
![](assets/2024-12-21-18-20-51.png)
**I flush privileges**
``` sh
FLUSH PRIVILEGES
```
![](assets/2024-12-21-18-36-53.png)  
**MOVE TO MYSQL-CLIENT**
**I SHOW IP**
```sh
sudo  ip addr show
```
**I modify the security group of the mysql-server to allow only the mysql-client to connect in the EC2**
![](assets/2024-12-21-18-46-59.png)
![alt text](sg.png)
**I moved back to mysql server to allow remote access in the configuration file**
``` sh
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```
![](ALLOW_REMOTE_CONF.png)
**I restart mysql**
``` sh
sudo systemctl restart mysql
```
![](assets/2024-12-21-18-54-31.png)
**I login from the mysql_client into mysql_server; a good example of the client-server architecture**
``` sh
mysql -u chuks -h 172.31.23.6 -p
```
![alt text](remote_login.png)