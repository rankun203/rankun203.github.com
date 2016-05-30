---
title: fonts.rankun.org
date: 2015-06-18 21:10:31
categories:
- webmaster
tags:
- google-fonts
- web-fonts
- nginx
---

## 搭建一个在国内外都可以访问的 Google Fonts 代理

> Google fonts is blocked in China.

-- by [Google Fonts Unstable in China – Here is How to Fix It](http://chineseseoshifu.com/blog/google-fonts-instable-in-china.html)

Yah, we all know that. But the general solution for this is awkward to me, Because after I switched the fonts location to http://fonts.useso.com, I can open my blog very quickly inside China, where the useso(360™) located. When I was trying to access it from the outside of China, both Japanese and West American are slow, over 5 seconds to download a 800 Bytes file, That's unbearable.

Then I tried to use Qiniu as a CDN to cache `fonts.googleapi.com`, then I realized it's blocked anyway. Afterwards, I use the CDN to cache fonts.useso.com, still doesn't work at all, it persist showing me this:

```
{
  error: "get from image source failed: E400"
}
```

<!-- more -->

Then I remember my server in L.A., That's it! Let's build a cache by ourselves!

Update nginx configuration to add the following lines:

```
server {
  server_name fontus.rankun.org
  listen 80 default_server;
  proxy_cache cache_zone;

  location / {
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://fonts.googleapis.com/;
  }
}
```

Then reload Nginx by `service nginx reload` if you are also using Ubuntu.

There you go, `fontus.rankun.org` will performs perfectly.

One last word, The Chinese International Export bandwidth is tooooooooooooo slow !
