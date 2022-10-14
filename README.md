
#v2ray-docker-nginx-dns

-----------

- [internal server](#internal server)

  - [git clone](#step-1)
  - [install nginx](#step-2)
  - [run docker-compose](#step-3)
  - [run certbot(let's encrypt)](#step-4)
  - [edit nginx and config ssl](#step-5)
  - [restart docker-compose ](#step-5)
-----

#internal server

##step 1

```console
git clone https://github.com/ahmadrezamansuory/docker-nginx-dns-ssl
cd docker-nginx-dns-ssl/
```

-----

## step 2 :

```bash
docker pull sameersbn/bind:latest
```

### edit `./bindconfig/example.com.zone`

### edit  `./bindconfig/named.conf`

## step 3 :

### pull image nginx

```bash
docker pull nginx:latest
```

###edit `./nginx/conf.d/default.conf`

-----

## step 3:

## run docekr compose

```bash
docker-compose up -d
```

## step 4:

### run certbot:

```bash
docker-compose run --rm  certbot certonly --webroot --webroot-path /var/www/certbot/ --dry-run -d example.com
```

```bash
docker-compose run --rm  certbot certonly --webroot --webroot-path /var/www/certbot/ -d --dry-run -d example.com
```
### check `./data/certbot/conf/live/` must directory with your domain created
## step 5:

###edit `./nginx/conf.d/default.conf` and remove comment line and edit example.com in there

```commandline
 ssl_certificate /etc/nginx/ssl/live/exampel.com/fullchain.pem;
 ssl_certificate_key /etc/nginx/ssl/live/exampel.com/privkey.pem;
```
## step 6:
```bash
docker-compose restart 
```
>>>>>>> 92cffd6 (Update README.md)
