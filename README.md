# LaraDock

[![forthebadge](http://forthebadge.com/images/badges/built-by-developers.svg)](http://zalt.me)

[![Gitter](https://badges.gitter.im/LaraDock/laradock.svg)](https://gitter.im/LaraDock/laradock?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

LaraDock helps you run your **Laravel** App on **Docker** real quick.
<br>
It's like Laravel Homestead but for Docker instead of Vagrant.

>With LaraDock, use Docker first and learn about it later.


![](https://s31.postimg.org/nbettdki3/lara_dock_poster_new.jpg)

<br>
## Contents


- [Intro](#Intro)
	- [Features](#features)
	- [Supported Software's](#Supported-Containers)
	- [What is Docker](#what-is-docker)
	- [What is Laravel](#what-is-laravel)
	- [Why Docker not Vagrant](#why-docker-not-vagrant)
	- [LaraDock VS Homestead](#laradock-vs-homestead)
- [Requirements](#Requirements)
- [Installation](#Installation)
- [Usage](#Usage)
- [Use custom Domain](#Use-custom-Domain)
- [Documentation](#Documentation)
	- [Docker](#Docker)
		- [List current running Containers](#List-current-running-Containers)
		- [Close all running Containers](#Close-all-running-Containers)
		- [Delete all existing Containers](#Delete-all-existing-Containers)
		- [Enter a Container (SSH into a running Container)](#Enter-Container)
		- [Edit default container configuration](#Edit-Container)
		- [Edit a Docker Image](#Edit-a-Docker-Image)
		- [Build/Re-build Containers](#Build-Re-build-Containers)
		- [Add more Software's (Docker Images)](#Add-Docker-Images)
		- [View the Log files](#View-the-Log-files)
- [Help & Questions](#Help)



<a name="Intro"></a>
## Intro

LaraDock strives to make the development experience easier.
It contains pre-packaged Docker Images that provides you a wonderful development environment without requiring you to install PHP, NGINX, MySQL, REDIS, and any other software on your local machine.


<a name="features"></a>
### Features

- Easy switch between PHP versions: 7.0, 5.6, 5.5...
- Choose your favorite database engine: MySQL, Postgres, MariaDB...
- Run your own combination of software's: Memcached, HHVM, Beanstalkd...
- Every software runs on a separate container: PHP-FPM, NGINX, PHP-CLI...
- Easy to customize any container, with simple edit to the `dockerfile`.
- All Images extends from an official base Image. (Trusted base Images).
- Pre-configured Nginx for Laravel.
- Easy to apply configurations inside containers.
- Clean and well structured Dockerfiles (`dockerfile`).
- Latest version of the Docker Compose file (`docker-compose`).
- Everything is visible and editable.
- Fast Images Builds.
- More to come every week..


<a name="Supported-Containers"></a>
### Supported Software's (Containers)

- **Database Engines:**
	- MySQL
	- PostgreSQL
	- MariaDB
	- MongoDB
	- Neo4j
- **Cache Engines:**
	- Redis
	- Memcached
- **PHP Servers:**
	- NGINX
	- Apache2
	- Caddy
- **PHP Compilers:**
	- PHP-FPM
	- HHVM
- **Message Queueing Systems:**
	- Beanstalkd (+ Beanstalkd Console)
- **Tools:**
	- Workspace (PHP7-CLI, Composer, Git, Node, Gulp, SQLite, Vim, Nano, cURL...)


>If you can't find your Software, build it yourself and add it to this list. Contributions are welcomed :)





<a name="what-is-docker"></a>
### What is Docker?

[Docker](https://www.docker.com) is an open-source project that automates the deployment of applications inside software containers, by providing an additional layer of abstraction and automation of [operating-system-level virtualization](https://en.wikipedia.org/wiki/Operating-system-level_virtualization) on Linux, Mac OS and Windows.

<a name="what-is-laravel"></a>
### What is Laravel?

Seriously!!!


<a name="why-docker-not-vagrant"></a>
### Why Docker not Vagrant!?

[Vagrant](https://www.vagrantup.com) creates Virtual Machines in minutes while Docker creates Virtual Containers in seconds.

Instead of providing a full Virtual Machines, like you get with Vagrant, Docker provides you **lightweight** Virtual Containers, that share the same kernel and allow to safely execute independent processes.

In addition to the speed, Docker gives tons of features that cannot be achieved with Vagrant.

Most importantly Docker can run on Development and on Production (same environment everywhere). While Vagrant is designed for Development only, (so you have to re-provision your server on Production every time).


<a name="laradock-vs-homestead"></a>
### LaraDock VS Homestead

LaraDock and [Homestead](https://laravel.com/docs/master/homestead) both gives you a complete virtual development environments. (Without the need to install and configure every single software on your own Operating System).

- Homestead is a tool that controls Vagrant for you (using Homestead special commands). And Vagrant manages your Virtual Machine.

- LaraDock is a tool that controls Docker for you (using Docker & Docker Compose official commands). And Docker manages your Virtual Containers.

Running a virtual Container is much faster than running a full virtual Machine. Thus **LaraDock is much faster than Homestead**.




<a name="Requirements"></a>
## Requirements

- [Git](https://git-scm.com/downloads)
- [Docker](https://www.docker.com/products/docker/)



<a name="Installation"></a>
## Installation


1 - Clone the `LaraDock` repository:

Clone this repository on your `Laravel` root direcotry:

```bash
git submodule add https://github.com/fgiannar/laradock.git
```



<a name="Usage"></a>
## Usage


**Read Before starting:**

If you are using **Docker Toolbox** (VM), do one of the following:

- Upgrade to Docker [Native](https://www.docker.com/products/docker) for Mac/Windows (Recommended). Check out [Upgrading Laradock](#upgrading-laradock)
- Use LaraDock v3.* (Visit the `LaraDock-ToolBox` [Branch](https://github.com/LaraDock/laradock/tree/LaraDock-ToolBox)).


If you are using **Docker Native** (For Mac/Windows) or even for Linux, continue this documentation normally since LaraDock v4 and above is just for that.



<br>
<br>
1 - Run Containers: *(Make sure you are in the `laradock` folder before running the `docker-compose` commands).*

Running Apache2 and MySQL:

```bash
docker-compose up -d apache2 mysql redis
```

You can select your own combination of Containers form the list below:

`nginx`, `hhvm`, `php-fpm`, `mysql`, `redis`, `postgres`, `mariadb`, `neo4j`, `mongo`, `apache2`, `caddy`, `memcached`, `beanstalkd`, `beanstalkd-console`, `workspace`.


**Note**: `workspace` and `php-fpm` will run automatically in most of the cases, so no need to specify them in the `up` command.

**Note**: If you prefer to use your local mysql instance, omit mysql from the above command.


<br>
**IMPORTANT**: Omit this step if you don't use the mysql container.

2 - Edit the Laravel configurations.

Open your Laravel's `.local` file and set the `DB_PORT` to your `3307`:

```env
DB_PORT=3307
```
<br>

3 - Enter the Workspace container, to execute commands like (Artisan, Composer, PHPUnit, Gulp, ...).

If you added mysql on step 2, you will need to enter the container in order to run the migrations and optionally seed:

```bash
docker-compose exec workspace bash
php artisan migrate
php artisan db:seed
```
<br />

Add `--user=laradock` (example `docker-compose exec --user=laradock workspace bash`) to have files created as your host's user. (you can change the PUID (User id) and PGID (group id) variables from the `docker-compose.yml`).

<br>
4 - Open your browser and visit your localhost address (`https://localhost:8001`).

<br>

5 - Use custom Domain (instead of the Docker IP)

Assuming your custom domain is `app.exitbee.docker`

a) Run:

```
sudo ifconfig lo0 10.0.0.1 alias
echo "rdr pass on lo0 inet proto tcp from any to 10.0.0.1 port 80 -> 127.0.0.1 port 8001" | sudo pfctl -ef -
```


b) Open your `/etc/hosts` file and map the alias address `10.10.0.1` to the `app.exitbee.docker` domain, by adding the following:

```bash
10.10.0.1 app.exitbee.docker
```

2 - Open your browser and visit `{https://app.exitbee.docker}`



<br>
**Debugging**: if you are facing any problem here check the [Debugging](#debugging) section.



<a name="List-current-running-Containers"></a>
### List current running Containers
```bash
docker ps
```
You can also use the this command if you want to see only this project containers:

```bash
docker-compose ps
```



<br>
<a name="Close-all-running-Containers"></a>
### Close all running Containers
```bash
docker-compose stop
```

To stop single container do:

```bash
docker-compose stop {container-name}
```






<br>
<a name="Delete-all-existing-Containers"></a>
### Delete all existing Containers
```bash
docker-compose down
```

*Note: Careful with this command as it will delete your Data Volume Container as well. (if you want to keep your Database data than you should stop each container by itself as follow):*







<br>
<a name="Enter-Container"></a>
### Enter a Container (SSH into a running Container)

1 - first list the current running containers with `docker ps`

2 - enter any container using:

```bash
docker-composer exec {container-name} bash
```

*Example: enter MySQL container*

```bash
docker-compose exec mysql bash
```

3 - to exit a container, type `exit`.







<br>
<a name="Edit-Container"></a>
### Edit default container configuration
Open the `docker-compose.yml` and change anything you want.

Examples:

Change MySQL Database Name:

```yml
  environment:
    MYSQL_DATABASE: laradock
```

Change Redis defaut port to 1111:

```yml
  ports:
    - "1111:6379"
```








<br>
<a name="Edit-a-Docker-Image"></a>
### Edit a Docker Image

1 - Find the `dockerfile` of the image you want to edit,
<br>
example for `mysql` it will be `mysql/Dockerfile`.

2 - Edit the file the way you want.

3 - Re-build the container:

```bash
docker-compose build mysql
```
More info on Containers rebuilding [here](#Build-Re-build-Containers).








<br>
<a name="Build-Re-build-Containers"></a>
### Build/Re-build Containers

If you do any change to any `dockerfile` make sure you run this command, for the changes to take effect:

```bash
docker-compose build
```
Optionally you can specify which container to rebuild (instead of rebuilding all the containers):

```bash
docker-compose build {container-name}
```

You might use the `--no-cache` option if you want full rebuilding (`docker-compose build --no-cache {container-name}`).





<br>
<a name="Add-Docker-Images"></a>
### Add more Software's (Docker Images)

To add an image (software), just edit the `docker-compose.yml` and add your container details, to do so you need to be familiar with the [docker compose file syntax](https://docs.docker.com/compose/compose-file/).









<br>
<a name="View-the-Log-files"></a>
### View the Log files
The Nginx Log file is stored in the `logs/nginx` directory.

However to view the logs of all the other containers (MySQL, PHP-FPM,...) you can run this:

```bash
docker logs {container-name}
```


<br>
<a name="Use-Redis"></a>
### Use Redis

1 - First make sure you run the Redis Container (`redis`) with the `docker-compose up` command.

```bash
docker-compose up -d redis
```

2 - Open your Laravel's `.env` file and set the `REDIS_HOST` to `redis`

```env
REDIS_HOST=redis
```

If you don't find the `REDIS_HOST` variable in your `.env` file. Go to the database config file `config/database.php` and replace the default `127.0.0.1` IP with `redis` for Redis like this:

```php
'redis' => [
    'cluster' => false,
    'default' => [
        'host'     => 'redis',
        'port'     => 6379,
        'database' => 0,
    ],
],
```

3 - To enable Redis Caching and/or for Sessions Management. Also from the `.env` file set `CACHE_DRIVER` and `SESSION_DRIVER` to `redis` instead of the default `file`.

```env
CACHE_DRIVER=redis
SESSION_DRIVER=redis
```

4 - Finally make sure you have the `predis/predis` package `(~1.0)` installed via Composer:

```bash
composer require predis/predis:^1.0
```

5 - You can manually test it from Laravel with this code:

```php
\Cache::store('redis')->put('LaraDock', 'Awesome', 10);
```



<br>
<a name="debugging"></a>
### Debugging

*Here's a list of the common problems you might face, and the possible solutions.*

#### I see a blank (white) page instead of the Laravel 'Welcome' page!

Run the following command from the Laravel root directory:

```bash
sudo chmod -R 777 storage bootstrap/cache
```

#### I see "Welcome to nginx" instead of the Laravel App!

Use `http://127.0.0.1` (or [your Docker IP](#Find-Docker-IP-Address)) instead of `http://localhost` in your browser.

#### I see an error message containing `address already in use`

Make sure the ports for the services that you are trying to run (80, 3306, etc.) are not being used already by other programs, such as a built in `apache`/`httpd` service or other development tools you have installed.



<br>
## Contributing

This little project was built by one man who has a full time job and many responsibilities, so if you like this project and you find that it needs a bug fix or support for new software or upgrade any container, or anything else.. Do not hesitate to contribute, you are more than welcome :)

#### Read our [Contribution Guidelines](https://github.com/LaraDock/laradock/blob/master/CONTRIBUTING.md)

<a name="Help"></a>
## Help & Questions

Join the chat room on [Gitter](https://gitter.im/LaraDock/laradock) and get help and support from the community.

You can as well can open an [issue](https://github.com/laradock/laradock/issues) on Github (will be labeled as Question) and discuss it with people on [Gitter](https://gitter.im/LaraDock/laradock).

For special help with Docker and/or Laravel, you can schedule a live call with the creator of this project at [Codementor.io](https://www.codementor.io/mahmoudz).

## Credits

**Creator:**

- [Mahmoud Zalt](https://github.com/Mahmoudz)  (Twitter [@Mahmoud_Zalt](https://twitter.com/Mahmoud_Zalt))

**Main Contributors:**

- [Eric Pfeiffer (computerfr33k)](https://github.com/computerfr33k)
- [Orette](https://github.com/orette)
- [Jack Fletcher (Kauhat)](https://github.com/Kauhat)
- [Bo-Yi Wu (appleboy)](https://github.com/appleboy)
- [Amin Mkh (AminMkh)](https://github.com/AminMkh)
- [Matthew Tonkin Dunn (mattythebatty)](https://github.com/mattythebatty)
- [Zhivitsa Kirill (zhikiri)](https://github.com/zhikiri)
- [Benmag](https://github.com/benmag)

**Awesome People:**

- [Contributors](https://github.com/LaraDock/laradock/graphs/contributors)
- [Supporters](https://github.com/LaraDock/laradock/issues?utf8=%E2%9C%93&q=)


## License

[MIT License](https://github.com/laradock/laradock/blob/master/LICENSE) (MIT)
