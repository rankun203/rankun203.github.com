title: 'Enable Google Drive file sync, on a Mac, in China'
date: 2016-04-05 19:35:56
tags:
- polipo
- ssh-tunnel
- http-proxy
- proxy
- google-drive
- google
- gfw
---

Use Polipo to convert a socks connection into a http proxy.

```
brew install polipo
```

Once you had polipo installed, config it to work properly with a `polipo.proxy`:

```
socksParentProxy = "localhost:8089"
socksProxyType = socks5

proxyAddress = "::0"        # both IPv4 and IPv6
# allowedClients = 127.0.0.1, 192.168.1.1/255

pmmFirstSize = 16384
pmmSize = 8192
```

And start polipo.

```
polipo -c ./polipo.config
```

Then config `Web Proxy (HTTP) & Secure Web Proxy (HTTPS)` to `127.0.0.1:8123` (Settings -> Network -> Advanced -> Proxies -> Web Proxy (HTTP) -> **OK** -> **Apply**).

And you will get your Google Drive sync each changes on the fly.

#### For convenient, use our bash tool :)

[Bash, OS X: pSet - a CLI, help you manage your OSX network settings.](https://github.com/rankun203/pset)

<script type="text/javascript" src="https://asciinema.org/a/bpg5gngmuzgqr9dcu6xrtoiqw.js" id="asciicast-bpg5gngmuzgqr9dcu6xrtoiqw" async></script>