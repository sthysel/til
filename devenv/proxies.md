# Docker proxy containers 

These proxies are hosted in containers. The proxies caches apt (squid) and pip (pypi)
packages and improves image building time.

## http squid proxy
```
 systemctl start squid.service
 systemctl status squid.service
```


## devpi pip proxy
```
 systemctl status devpi.service
 systemctl start devpi.service
```

```
$ docker ps                         
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                                                                          NAMES
63871f5c9273        muccg/devpi:latest             "/docker-entrypoint.s"   7 minutes ago       Up 7 minutes        0.0.0.0:3141->3141/tcp                                                         devpi.service
4c9b20ab37ac        muccg/squid-deb-proxy:latest   "/docker-entrypoint.s"   7 minutes ago       Up 7 minutes        0.0.0.0:3128->8000/tcp                                                         squid.service
```

