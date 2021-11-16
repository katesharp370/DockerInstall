# Docker Install

This outlines the installation of Docker on Ubuntu and how to set up WordPress with it.

## Installing Docker on Ubuntu

```
sudo apt update
```

* install proper https packages

  ```
  sudo apt install apt-transport-https ca-certificates curl software-properties-common
  ```

* install gpg key for the Docker repo

  ```
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  ```

* add the Docker APT repo 

  ```
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
  ```

* Run upate command again

  ```
  sudo apt update
  ```

* install Docker

  ```
  sudo apt install docker-ce docker-ce-cli containerd.io
  ```

* check docker is running (if it says "active" then everything is Gucci)

  ```
  systemctl is-active docker
  ```

## Installing and Configuring WordPress
* Note: I had to use sudo in front of all these because I did not add users to a docker group

* Install Docker Compose

  ```
  sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  ```

* Change Executable Bits

  ```
  sudo chmod +x /usr/local/bin/docker-compose
  ```

* Check the installation

  ```
  docker-compose --version
  ```

* Create Directory for Wordpress Containter
  ```
  sudo mkdir -p /srv/wordpress
  ```
* I had to sign-in as root to do this part, so I used:
```sudo -i```
  * Enter directory we just created
  ```cd /srv/wordpress```
  * Install Vim (If needed)
  ```apt install vim```
  * Create docker-compose.yaml file:
  ```vim docker-compose.yaml```
  * Copy and paste this config
  
  ```
    version: '3'
    services:
    mysql:
    image: mysql:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: my_password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress_user
      MYSQL_PASSWORD: wordpress_password
    volumes:
      - mysql_data:/var/lib/mysql
    wordpress:
    image: wordpress:latest
    depends_on:
      - mysql
    ports:
      - 8080:80
    restart: always
    environment:
      WORDPRESS_DB_HOST: mysql:3306
      WORDPRESS_DB_USER: wordpress_user
      WORDPRESS_DB_PASSWORD: wordpress_password
    volumes:
      - ./wp-content:/var/www/html/wp-content
    volumes:
    mysql_data:
  ```
 * Switch back to your normal user and run
 ```
 sudo docker-compose up -d
 ```
 * After successful completion you should be able to access the WordPress admin site at:
 ```
 http://localhost:8080/
 ```
 
 * Complete the account creation and log in, you're done!

