title: Ultimate docker on OSX collection - mapping docker files to local
date: 2016-03-28 22:07:25
tags:
- docker
- sshfs
- osx
---

Yes, you've heard, and have looked around [here][1], [here][2], or [maybe][3] [here][4], it's different to Linux with a simple volume mapped to your local machine. In OSX world, Docker is working in a VirtualBox…

So the file permission got be a problem, you can't simply change its group or permission, neither. let's fix it.

The idea is like this: 

- Everything in Docker operate as normal.
- Create a new docker container that serves a ssh endpoint.
- Connect to that ssh point, and get access to the file system inside our docker.
- Get deeper, map the files of docker volume to local file system.

### Let's get started.

Run your containers as normal.

Go to your docker-compose directory, edit the file `docker-compose.yml`.

```
sshd:
  image: 'krlmlr/debian-ssh'
  ports:
    - '2222:22'
  environment:
    - SSH_KEY=ssh-rsa AAAAxxxx_ssh_rsa_pub_content rankun203@gmail.com
  volumes_from:
    - data
  working_dir: /var/www/html
```

Run it

```
docker-compose up sshd
```

Mount the docker file system to your local file system:

```
sshfs -p 2222 root@youdar.dev:/var/www/html ~/docker/nhweb -oauto_cache,reconnect,defer_permissions,noappledouble,negative_vncache,volname=nhweb
```

Notes:

- `volname=nhweb` is the *directory name* of the mount point.
- `~/docker/nhweb` is the mount point.
- These options are selected for more friendly and less errors.

Now your local folder `~/docker/nhweb` are just the same as inside the Docker, but with the right access rights.

Notes:

- All the file created by you will on the name of root user inside the docker.
- If you want to use another limited user with sudo permission, use `docker`.

References:

- [Another guide][5]
- [SSHFS Home page][6]
- [Download SSHFS][7]

[1]: https://forums.docker.com/t/docker-toolbox-host-folder-permissions/3419/7
[2]: https://github.com/boot2docker/boot2docker/issues/587
[3]: https://github.com/boot2docker/boot2docker/issues/581
[4]: https://gist.github.com/codeinthehole/7ea69f8a21c67cc07293
[5]: https://blogs.harvard.edu/acts/2013/11/08/the-newbie-how-to-set-up-sshfs-on-mac-os-x/
[6]: https://github.com/osxfuse/sshfs
[7]: https://github.com/osxfuse/sshfs/releases
