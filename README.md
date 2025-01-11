# Basic Authentication Squid Docker

Minimal docker image with [Squid] that only proxies authenticated requests and (optionally) only to certain domains.

### Usage

Build the Docker Image

```
docker compose build
```

Create the new container from the squid-auth:1.0 image

```sh
# generate your username and password
USERNAME=user
PASSWORD=$(openssl rand -hex 16)

# run your instance
docker run -d --name squid -e PROXY_USERNAME=$USERNAME -e PROXY_PASSWORD=$PASSWORD -p 3128:3128 snomiao/squid-auth

# When accessing the proxy, proxy user will be ```PROXY_USERNAME```, and password will be whatever you set in ```PROXY_PASSWORD```

HTTP_PROXY="http://$USERNAME:$PASSWORD@localhost:3128"

echo === test with
echo curl -x $HTTP_PROXY https://ifconfig.me
echo ===
echo

curl -x $HTTP_PROXY https://ifconfig.me
```



License
----

BSD

   [squid]: <http://www.squid-cache.org/>
