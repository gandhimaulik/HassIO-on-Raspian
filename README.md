# HassIO-on-Raspian
Home Assistant , HASS.io on Rasppian Buster on Raspberry Pi4


## Requirements

```
docker-ce
bash
jq
curl
avahi-daemon
dbus
```

**Important**: Don't only install NetworkManager, you need also use it on your system.

## Optional

```
apparmor-utils
network-manager
```


## Commands

### Get docker-ce
```
curl -sSL https://get.docker.com | sh
```
### Install dependacies
```
sudo apt-get install bash jq curl avahi-daemon dbus software-properties-common apparmor-utils network-manager
```
### Install HassIO
```
curl -sL https://raw.githubusercontent.com/home-assistant/hassio-installer/master/hassio_install.sh | bash -s -- -m raspberrypi4
```

## Setting up Apache reverse proxy

### Install apache and plugins

```
sudo apt install apache2
sudo a2enmod rewrite
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_wstunnel
```

### Adding entry in Apache site-enabled

Below lines need to be added in sites enabled configuration file. Path in Ubuntu is ``` /etc/apache2/sites-enabled/000-default.conf```

```
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        ServerName example.com
        RewriteEngine On
        RewriteCond %{HTTP:Upgrade} =websocket [NC]
        RewriteRule /(.*)           ws://127.0.0.1:44400/$1 [P,L]
        RewriteCond %{HTTP:Upgrade} !=websocket [NC]
        RewriteRule /(.*)           http://127.0.0.1:44400/$1 [P,L]
        ProxyPreserveHost On
        ProxyPass / http://127.0.0.1:44400/
        ProxyPassReverse / http://127.0.0.1:44400/
	      ErrorLog ${APACHE_LOG_DIR}/error.log
</VirtualHost>
```

Restart Apache server
```
sudo systemctl apache2 restart
```
