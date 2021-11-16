# Docker Install

## Installing Docker on Ubuntu

``` sudo apt update ```

* install packages

```sudo apt install apt-transport-https ca-certificates curl software-properties-common```

* install gpg key

```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```

* add the docker repo 

  ```sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"```

* verify install from the Docker repo

```apt-cache policy docker-ce```

* install Docker

```sudo apt install docker-ce```

* check docker is running

```sudo systemctl status docker```

## Installing OpenVas
* Note: I had to use sudo in front of all these because I did not add users to a docker group

```docker run -d -p 443:443 --name openvas mikesplain/openvas:9```
    

### header 2

* point
* point
* point


  
