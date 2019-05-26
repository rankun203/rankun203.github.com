title: Browse the Internet from China
date: 2016-04-04 17:48:52
tags:
- ssh
- ssh-tunnel
- autossh
- port-forwarding
- internet
- google
---

Updates:

- 2016-05-27 14:25:20
  - Docker enthusiast? (7MB/s)

Let's talk about network. Chinese version.

```bash
ssh -v -N -C -D 8089 -o ServerAliveInterval=60 -o ServerAliveCountMax=2048 rankun.org
```

One step further.

Before long, your will see a lot of error messages like this:

```bash
debug1: Connection to port 8089 forwarding to socks port 0 requested.
debug1: channel 24: new [dynamic-tcpip]
debug1: channel 24: free: dynamic-tcpip, nchannels 35
debug1: Connection to port 8089 forwarding to socks port 0 requested.
debug1: channel 24: new [dynamic-tcpip]
debug1: channel 24: free: dynamic-tcpip, nchannels 35
```

Which means your just lost the connection to remote server, but you can [use autossh to monitor and restart it][1].

```bash
autossh -M 2000 -v -N -C -D 8089 -o ServerAliveInterval=60 -o ServerAliveCountMax=2048 rkus.rankun.org
```

#### 3-tier forwarding

Idea: shadowsocks + port forwarding (ssh tunnel)

```bash
# Start a ssserver in a server outside of China (here: listen on oversea:993)
ssserver -c /path/to/config.json

# Setup a Chinese Cloud server, connect to that ssserver (rkus.json pointing to oversea:993 and listen on cloud:993)
sslocal -c rkus.json

# Finally, connect to cloud server at local (socks on local:8089, local forwarding to cloud:993)
ssh -v -C -N -L 8089:localhost:993 cloud

# If you want the local ssh port forwarding to be auto restart, try autossh
autossh -M 2000 -v -C -N -L 8089:localhost:993 -o ServerAliveInterval=60 -o ServerAliveCountMax=2048 sax.mindfine.com
```

The result?

Might surprise you :-)

~~OK, attached the video ;)~~

Step closer to development:

```bash
~/docker/nhweb on  master ⌚ 1:08:21
$ git push -uf origin master
Counting objects: 5993, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (5698/5698), done.
Writing objects: 100% (5993/5993), 29.00 MiB | 5.17 MiB/s, done.
Total 5993 (delta 627), reused 1422 (delta 120)
To https://youdar@bitbucket.org/youdarnet/nanhai-wp.git
 + 1b34252...dc448a1 master -> master (forced update)
Branch master set up to track remote branch master from origin.
```

Push code to Bitbucket (that one, normally 10-20KB/s...) can be up to 6MB/s.

Test environment: 四川省 长城宽带...

Notes:

- You will need 2 servers or at least ¥50 in your pocket to rent one.
- Some Internet are bad enough, in such condition, you will need to use a `AUTOSSH_POLL` env to force autossh check the connection health more frequent. Let's do a checking every 5 seconds!
  ```
  export AUTOSSH_POLL=5 &&  autossh -M 2000 -v -g -C -N -L 8089:localhost:993 -o ServerAliveInterval=60 -o ServerAliveCountMax=2048 hz.youdar.net
  ```

Thank you for reading,
Regards,
[Youdar][2]

[1]: http://www.debianadmin.com/autossh-automatically-restart-ssh-sessions-and-tunnels.html
[2]: http://youdar.net