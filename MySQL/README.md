# MySQL 

## MySql installation

1. 

```
sudo apt update
```

2. 

```
sudo apt install mysql-server
```

3. it has to be active

```
sudo systemctl status mysql
```

4. if not

```
systemctl start mysql
```

5. if you want to disable booting with boot

```
sudo systemctl disable mysql
```

6. if you want to enable boot with boot

```
sudo systemctl enable mysql
```

7. if you haven't created a password just use the command and press enter with the empty password

```
sudo mysql -u root -p
```

8. to create a user with sudo permissions and create the password

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'sua_senha_aqui'; flush privileges;
```

## MySQL uninstall

1. remove all installed packages

```
sudo apt-get remove mysql-server mysql-client mysql-common
```

2. remove dependencies files that are no longer needed, then remove old versions of package files

```
sudo apt-get autoremove
```

```
sudo apt-get autoclean
```

3. remove mysql files that may have been left behind

```
sudo rm -rf /var/lib/mysql
```

```
sudo rm -rf /etc/mysql
```

4. macOS

```
brew uninstall mysql
# ou
brew remove mysql
```

## download mySQL GUI

[mySQL](https://dev.mysql.com/downloads/workbench/)

1. 

```
sudo apt install ./nome-do-arquivo
#ex no Ubuntu 20.04: sudo apt install ./mysql-workbench-community_8.0.21-1ubuntu20.04_amd64.deb
```
