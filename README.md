# Vagrantfile that runs  2 VM with MysSQL / PHPMyAdmin installer

Vagrantfile with config for creating  2 VM based on Debian 11 (one with mysql the other with phpmyadmin) 

## 1. Requirements
 1) Vagrant must be installed on your pc\
 [Installing Vagrant](https://www.vagrantup.com/docs/installation)

 2) Install the plugin:
 ```sh
vagrant plugin install vagrant-env
```



## 2. Project configuration

Start by cloning this project on your workstation.

```sh
git@github.com:vlmaslennikov/
```

Run script `mysql-phpmyadmin-install.sh` with superuser rights

```sh
cd ./vagrant_mysql-phpmyadmin

vagrant up
```

Script launched by vagrant downloads and runs mysql and phpmyadmin installation script from private repository https://github.com/vlmaslennikov/mysql-phpmyadmin

### Environment variables :
\
All environment variables you can find in 
`.env`  and `.example.env` 
```
.example.env

# ########################## Vagrant config ######################################

# ########################## Global ##############################################
VM_BOX=generic/debian11

# ########################## PHPMyAdmin arguments ################################
# 1st arg:
PHPMYADMIN_PASSWORD=password1
# 2nd arg:
MYSQL_USER_NAME=user
# 3d arg:
MYSQL_USER_PASSWORD=password2
# 4th arg:
MYSQL_DB_NAME=some_db
# 5th arg:
MYSQL_HOST=localhost

# ########################## MySQL arguments #####################################
# 1st arg:
MYSQL_USER_PASSWORD=password2
# 2nd arg:
MYSQL_ROOT_PASSWORD=password3

```
 

### After successfully running vagrant :
\
 Upon successful completion of the installation script, the user credentials and connection information will be displayed in the console

VM with mysql:
 ``` 
MYSQL ROOT NAME - root
MYSQL ROOT PASSWORD - root
MYSQL USER NAME - newuser
MYSQL USER PASSWORD - password1
MYSQL DB NAME - new_db
MYSQL port - 3306
ALLOWED IP ADRESS FOR MYSQL - 127.0.0.1
```
VM with phpmyadmin:
```
PHPMYADMIN USER PASSWORD - password2
PHPMYADMIN URL - http://localhost/phpmyadmin/
 ```

### Connecting to VM:
\
VM with mysql:
 ``` 
vagrant ssh mysql
```
VM with phpmyadmin:
```
vagrant ssh phpmyadmin
 ```

## 3. Useful links
[Vagrant Documentation](https://www.vagrantup.com/docs)

[MysSQL / PHPMyAdmin installer](https://github.com/vlmaslennikov/mysql-phpmyadmin) 



  