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
sudo apt-get install bash jq curl avahi-daemon dbus software-properties-common apparmor-utils
```
### Install HassIO
```
curl -sL https://raw.githubusercontent.com/home-assistant/hassio-installer/master/hassio_install.sh | bash -s -- -m raspberrypi4
```
