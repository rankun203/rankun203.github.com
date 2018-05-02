title: SSH to overseas server too slow?
date: 2016-04-07 05:39:43
tags:
- ssh
- sshfs
---

### UPDATE (2018-05-03):

I ended up using a [BandWagon VPS](https://bwh1.net/cart.php) as high volume traffic proxy with an [AEAD encryption method](https://tools.ietf.org/html/rfc7539) and another faster one as a backup instead of those ssh forwarding stuff, it was unstable and quickly fallen only one month later and never be fast again.

----

_The original post:_

Use China mainland cloud server as a hop.

```
ssh -v -N -L 2222:remote.oversea:2222  cloud.mainland
```

Then:

```
ssh -p 2222 root@localhost
```

Or even mount as a local folder:

```
sshfs -p 2222 root@localhost:/var/www/html ~/docker/nhweb -oauto_cache,reconnect,defer_permissions,noappledouble,negative_vncache,volname=nhweb
```

#### A few sweet ssh features to improve your development experience.

Expose local port to internet with a delegate:

```
# Remote server
sudo vi /etc/ssh/sshd_config
# Append below content: 
# GatewayPorts yes

# Local
ssh -v -N -R *:9090:localhost:8080 cloud.mainland
```

Then heading to http://cloud.mainland:9090 for the results.

Ref:

- [SSH端口转发（隧道）](http://linux-wiki.cn/wiki/SSH%E7%AB%AF%E5%8F%A3%E8%BD%AC%E5%8F%91%EF%BC%88%E9%9A%A7%E9%81%93%EF%BC%89)
- https://help.ubuntu.com/community/SSH/OpenSSH/PortForwarding

Thanks for reading,
Regards,
Kun