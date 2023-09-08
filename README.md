# laravel-deploy

## NGINX
```shell
sudo apt update
sudo apt install nginx
sudo systemctl reload nginx
```


## MYSQL
```shell
sudo apt install mysql-server
```

```shell
sudo mysql
```

```mysql
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

```shell
sudo mysql_secure_installation
```

```mysql
CREATE USER 'username'@'host' IDENTIFIED WITH mysql_native_password BY 'password';
```

```mysql
CREATE DATABASE laravel;
```

```mysql
GRANT ALL ON laravel.* TO 'laravel'@'localhost';
```

```mysql
FLUSH PRIVILEGES;
```

## PHP-FPM-8.2

```shell
sudo apt update && sudo apt install -y software-properties-common
```

```shell
sudo add-apt-repository ppa:ondrej/php
```

```shell
sudo apt update
```

```shell
sudo apt install php8.2-fpm
```


## GIT

```shell
sudo apt install git
```

## COMPOSER
```shell
sudo apt install php-cli unzip
```

```shell
cd ~
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
HASH=`curl -sS https://composer.github.io/installer.sig`
echo $HASH

php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

## composer
```shell
composer -v
```


## NODE NPM
```shell
sudo apt-get update

sudo apt-get install -y ca-certificates curl gnupg

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
```


## NODE_MAJOR=20

```shell
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

sudo apt-get update

sudo apt-get install nodejs -y
```


## PHP Extensions

```shell
sudo apt-get install -y php-common php-mysql php-zip php-gd php-mbstring php-curl php-xml php-bcmath

```

```mysql
sudo apt-get install php-xml
sudo apt-get install php-curl
sudo apt-get install php-mysql
```
