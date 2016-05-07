# LaraDock

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://www.zalt.me)


LaraDock helps you run your **Laravel** App on **Docker** real quick.
<br>
It's like Laravel Homestead but for Docker instead of Vagrant.


![](http://s18.postimg.org/fhykchl09/new_laradock_cover.png)

<br>
## Contents


- [Intro](#Intro)
- [Default Containers](#Default-Containers)
- [Requirements](#Requirements)
- [Installation](#Installation)
- [Usage](#Usage)
- [Documentation](#Documentation)
	- [List current running Containers](#List-current-running-Containers)
	- [Close all running Containers](#Close-all-running-Containers)
	- [Delete all existing Containers](#Delete-all-existing-Containers)
	- [Build/Re-build Containers](#Build-Re-build-Containers)
	- [Use Redis in Laravel](#Use-Redis-in-Laravel)
	- [Use custom Domain](Use-custom-Domain)
	- [Change the PHP Version](#Change-the-PHP-Version)
	- [Add/Remove a Docker Container](#AddRemove-a-Docker-Container)
	- [Add more Software's (Docker Images)](#Add-Docker-Images)
	- [Edit a Docker Container](#Edit-a-Docker-Container)
	- [View the Log files](#View-the-Log-files)
	- [Enter a Container (SSH into a running Container)](#Enter-Container)
	- [Edit a Docker Image](#Edit-a-Docker-Image)
	- [Run a Docker Virtual Host](#Run-Docker-Virtual-Host)
	- [Find your Docker IP Address](#Find-Docker-IP-Address)





<a name="Intro"></a>
## Intro

LaraDock strives to make the development experience easier.
It contains pre-packaged Docker Images that provides you a wonderful development environment without requiring you to install PHP, NGINX, MySQL, REDIS, and any other software on your local machine.



### What is Docker?

[Docker](https://www.docker.com)  is an open-source project that automates the deployment of applications inside software containers, by providing an additional layer of abstraction and automation of [operating-system-level virtualization](https://en.wikipedia.org/wiki/Operating-system-level_virtualization) on Linux, Mac OS and Windows.

### What is Laravel?

Seriously!!!

### Why Docker not Vagrant!?
[Vagrant](https://www.vagrantup.com) gives you Virtual Machines in minutes while Docker gives you Virtual Containers in seconds.

Instead of providing a full Virtual Machines, like you get with Vagrant, Docker provides you **lightweight** Virtual Containers, that share the same kernel and allow to safely execute independent processes.


<a name="Default-Containers"></a>
## Default Containers

- PHP
- NGINX
- MySQL
- Redis
- Data Volume


<a name="Requirements"></a>
## Requirements
- Laravel ([Download](https://laravel.com/docs/master/installation))
- Docker Toolbox ([Download](https://www.docker.com/toolbox))
- Git ([Download](https://git-scm.com/downloads))
- Composer ([Download](https://getcomposer.org/download/))

<a name="Installation"></a>
## Installation

1 - Clone the `LaraDock` repository, in any of your `Laravel` projects:

```bash
git clone https://github.com/LaraDock/laradock.git docker
```

Instead of `git clone` you can use `git submodule add` in case you are already using Git for your Laravel project *(Recommended)*:

```bash
git submodule add https://github.com/LaraDock/laradock.git docker
```

>These commands should create a `docker` folder, on the root directory of your Laravel project.


<a name="Usage"></a>
## Usage

>**(Windows & MAC users)** Make sure you have a running Docker Virtual Host on your machine first. 
><br>
>[How to run a Docker Virtual Host?](#Run-Docker-Virtual-Host)


<br>
1 - Open your Laravel's `.env` file and set the `DB_HOST` to your `{Docker-IP}`:

```env
DB_HOST=xxx.xxx.xxx.xxx
```
[How to find my Docker IP Address?](#Find-Docker-IP-Address)

<br>
2 - Run the containers: 
<br>
*(Make sure you are in the `docker` folder before running this command)*

```bash
docker-compose up -d
```

>*Only the first time you run this command, it will take up to 5 minutes (depend on your connection speed) to download the Docker Images on your local machine.*

<br>
3 - Open your browser and visit your `{Docker-IP}` address (`http://xxx.xxx.xxx.xxx`).


> **Debugging**: in case you faced an error here, run this command from the Laravel root directory:
> <br>
> `sudo chmod -R 777 storage && sudo chmod -R 777 bootstrap/cache`

<br>


[Follow @Mahmoud_Zalt](https://twitter.com/Mahmoud_Zalt)




<br>
<a name="Documentation"></a>
## Documentation

<a name="List-current-running-Containers"></a>
#### List current running Containers
```bash
docker ps
```

<br>
<a name="Close-all-running-Containers"></a>
#### Close all running Containers
```bash
docker-compose stop
```

<br>
<a name="Delete-all-existing-Containers"></a>
#### Delete all existing Containers
```bash
docker-compose rm -f
```

*Note: Careful with this command as it will delete your Data Volume Container as well. (if you want to keep your Database data than you should stop each container by itself as follow):* 

`docker stop {container-name}`


<br>
<a name="Build-Re-build-Containers"></a>
#### Build/Re-build Containers
```bash
docker-compose build
```



<br>
<a name="Use-Redis-in-Laravel"></a>
#### Use Redis in Laravel

Open your Laravel's `.env` file and set the `REDIS_HOST` to your `Docker-IP` instead of the default `127.0.0.1` IP.

```env
REDIS_HOST=xxx.xxx.xxx.xxx
```

If you don't find the `REDIS_HOST` variable in your `.env` file. Go to the database config file `config/database.php` and replace the default `127.0.0.1` IP with your `Docker-IP` for Redis like this:

```php
'redis' => [
    'cluster' => false,
    'default' => [
        'host'     => 'xxx.xxx.xxx.xxx',
        'port'     => 6379,
        'database' => 0,
    ],
],
```

To enable Redis Caching and/or for Sessions Management. Also from the `.env` file set `CACHE_DRIVER` and `SESSION_DRIVER` to `redis` instead of the default `file`.

```env
CACHE_DRIVER=redis
SESSION_DRIVER=redis
```

Finally make sure you have the `predis/predis` package `(~1.0)` installed via Composer first.

```bash
composer require predis/predis:^1.0
```

You can manually test it with:

```php
\Cache::store('redis')->put('laradock', 'awesome', 10);
```


<br>
<a name="Use-custom-Domain"></a>
#### Use custom Domain (instead of the Docker IP)

Assuming your custom domain is `laravel.dev` and your current `Docker-IP` is `xxx.xxx.xxx.xxx`.

1 - Open your `/etc/hosts` file and map your `Docker IP` to the `laravel.dev` domain, by adding the following:

```bash
xxx.xxx.xxx.xxx    laravel.dev
```

2 - Open your Laravel's `.env` file and replace the `127.0.0.1` default values with your `{Docker-IP}`.
<br>
Example:

```env
DB_HOST=xxx.xxx.xxx.xxx
```

3 - Open your browser and visit `{http://laravel.dev}`



Optionally you can define the server name in the nginx config file, like this:

```
server_name laravel.dev;
```



<br>
<a name="Change-the-PHP-Version"></a>
#### Change the PHP Version
By default **PHP 7.0** is running.
<br>
To change the default PHP version:

1 - Open the `dockerfile` of the `php` folder.

2 - Change the PHP version number in the first line,

```txt
FROM php:7.0-fpm
```

Supported Versions:

- For (PHP 7.0.*) use `php:7.0-fpm`
- For (PHP 5.6.*) use `php:5.6-fpm`
- For (PHP 5.5.*) use `php:5.5-fpm`

For more details visit the [official PHP docker images](https://hub.docker.com/_/php/).


<br>
<a name="Add-Docker-Images"></a>
#### Add more Software's (Docker Images)

To add an image (software), just edit the `docker-compose.yml` and add your container details, to do so you need to be familiar with the [docker compose file syntax](https://docs.docker.com/compose/compose-file/).



<br>
<a name="Edit-a-Docker-Container"></a>
#### Edit a Docker Container (change Ports or Volumes)
To modify a container you can simply open the `docker-compose.yml` and change everything you want.

Example: if you want to set the MySQL port to 3333, just replace the default port with yours:

```yml
  ports:
    - "3333:3306"
```



<br>
<a name="View-the-Log-files"></a>
#### View the Log files 
The Log files are stored in the `docker/logs` directory.


<br>
<a name="Enter-Container"></a>
#### Enter a Container (SSH into a running Container)

1 - first list the current running containers with `docker ps`

2 - enter any container with:

Example: enter the `php` container

```bash
docker exec -it php bash
```

Example: enter the `nginx` container

```bash
docker exec -it nginx bash
```



<br>
<a name="AddRemove-a-Docker-Container"></a>
#### Add/Remove a Docker Container
To prevent a container (software) from running, open the `docker-compose.yml` file, and comment out the container section or remove it entirely.



<br>
<a name="Edit-a-Docker-Image"></a>
#### Edit a Docker Image

1 - Find the `dockerfile` of the image you want to edit, 
<br>
example for `php` it will be `docker/php/dockerfile`.

2 - Edit the file the way you want.

3 - Re-build the container:

```bash
docker-compose build
```

*If you find any bug or you have and suggestion that can improve the performance of any image, please consider contributing. Thanks in advance.*




<br>
<a name="Run-Docker-Virtual-Host"></a>
#### Run a Docker Virtual Host

These steps are only for **Windows & MAC** users *(Linux users don't need a virtual host)*:

1 - Run the default Host:

```bash
docker-machine start default
```

* If the host "default" does not exist, create one using the command below, else skip it:

* ```bash
  docker-machine create -d virtualbox default
  ```

2 - Run this command to configure your shell:

```bash
eval $(docker-machine env)
```



<br>
<a name="Find-Docker-IP-Address"></a>
#### Find your Docker IP Address 

**On Windows & MAC:** 

```bash
docker-machine ip default
```
*(The default IP is 192.168.99.100)*

**On Linux:** 

Your IP Address is `127.0.0.1`

> **boot2docker** users: run `boot2docker ip` *(when boot2docker is up)*.




<br>
## Contributing

This little project was built by one man who has a full time job and many responsibilities, so if you like this project and you find that it needs a bug fix or support for new software or upgrade for the current containers, or anything else.. Do not hesitate to contribute, you are more than welcome :)

All Docker Images can be found at [https://github.com/LaraDock](https://github.com/LaraDock)

## Support

[Issues](https://github.com/laradock/laradock/issues) on Github.



### Questions?
If you have any question, send me a direct message on LaraChat, my username is `mahmoud_zalt`.


## Credits

[![Mahmoud Zalt](https://img.shields.io/badge/Author-Mahmoud%20Zalt-orange.svg)](http://www.zalt.me)



## License

[MIT License (MIT)](https://github.com/laradock/laradock/blob/master/LICENSE)
[]([]())