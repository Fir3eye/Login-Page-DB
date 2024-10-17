## Install MySQL on the EC2 Instance
```
sudo apt update
sudo apt install mysql-server -y
```

## Configure MySQL
- Start the MySQL service
```
sudo systemctl start mysql
sudo systemctl enable mysql
```
- Set the MySQL root password:
```
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
FLUSH PRIVILEGES;
```
- Create the database and table:
```
CREATE DATABASE mydb;
USE mydb;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL
);

```
### Step-4. Create a new MySQL user 
```
CREATE USER 'root'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON mydb.* TO 'root'@'%';
FLUSH PRIVILEGES;
```
## Allow Remote Connections to MySQL
- Edit the MySQL configuration file:
```
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```
- Change it to:
```
bind-address = 0.0.0.0
```
- Restart MySQL:
```
sudo systemctl restart mysql
```



## Run Your Flask App
- Install the required Python packages:
```
pip install flask mysql-connector-python werkzeug

```
- Start the Flask application:
```
python app.py
```