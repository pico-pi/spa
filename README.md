## Modifications to the standard Raspberry Pi Lite OS

### Enable SSH
sudo touch boot/ssh

### Configure Wifi
sudo nano etc/wpa_supplicant/wpa_supplicant.conf
```
country=FR
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="wifi name"
    psk="wifi password"
    key_mgmt=WPA-PSK
    priority=1
}
network={
    ssid="wifi name"
    psk="wifi password"
    key_mgmt=WPA-PSK
    priority=2
}

```
