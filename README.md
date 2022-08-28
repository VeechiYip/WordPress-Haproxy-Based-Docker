# Overview
This is the Git repo to build [`wordpress`](https://hub.docker.com/_/wordpress/) + SSL easily by using [`Docker-Compose`](https://docs.docker.com/compose/).

All image are pull from Docker Offical-Image.

## Step.1 - Ready to Build
Firstly, you may need to install docker from offical channel

```Bash
curl -fsSL get.docker.com -o get-docker.sh
```

## Step.2 - Edit Source
There are two thing you need replace
1. In haproxy.cfg, edit your wordpress domain
```
use_backend WORDPRESS	if { ssl_fc_sni -i {YOUR_WORDPRESS_DOMAIN} }
```
2.In all.pem
Place your cert & key value

## Step.3 - Install
In project path
```Bash
docker compose up
```
or
```Bash
docker-compose up
```

If you installed docker by Step.1. Docker compose are build-in. If not,you may need to install docker compose. Go to [`INSTALL`](https://docs.docker.com/compose/install/)

## TroubleShooting
You may realize that JS/CSS style are lossing. Here is how to fix it:

1.Check Wordpress Container ID
```Bash
docker ps
```
2.Enter Wordpress Container
```Bash
docker exec -it {Wordpress Container ID} bash
```
3.Edit wp-config.php.  Install one of vi/vim if command not found
```Bash
vim wp-config.php
```
4. add three line code in the location behind */ and save.
```PHP
 * @package WordPress
 */
$_SERVER['HTTPS'] = 'on';
define('FORCE_SSL_LOGIN', true);
define('FORCE_SSL_ADMIN', true);
```
