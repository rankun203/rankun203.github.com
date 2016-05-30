title: Ultimate Docker on OSX collection - debug PHP application
date: 2016-03-28 22:04:31
tags:
- docker
- osx
- sshfs
---

With IntelliJ IDEA

PHP Docker debugging:

See this link to install xdebug:

- http://stackoverflow.com/a/33373411/1904043

Configure your IDE, listen on income debug request, create php server, debug session:

- https://gist.github.com/chadrien/c90927ec2d160ffea9c4

**Restart your docker with `docker-compose restart nhweb`**


### The Steps:

<!-- more -->

1. Get in to your docker running container:

```
docker exec -it container_name /bin/bash

pecl install xdebug
docker-php-ext-enable xdebug
sed -i '1 a xdebug.remote_autostart=true' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
sed -i '1 a xdebug.remote_mode=req' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
sed -i '1 a xdebug.remote_handler=dbgp' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
sed -i '1 a xdebug.remote_connect_back=1 ' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
sed -i '1 a xdebug.remote_port=9000' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
sed -i '1 a xdebug.remote_host=127.0.0.1' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
sed -i '1 a xdebug.remote_enable=1' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
```

2. Restart your container:

```
# Docker composer
docker-compose restart nhweb
```

3. In Intellij/PHPStorm go to: Languages & Frameworks > PHP > Debug > DBGp Proxy and set the following settings:

- Host: your IP address
- Port: 9000

4. Add remote debug in your `Run/Debug Configuration`
  - Add server, map directory

5. Debug it to start the debug session.
6. Put a breakpoint in your index.php, open the browser.
