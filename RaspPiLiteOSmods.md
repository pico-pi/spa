After creating the :floppy_disk: SD image from www.raspberrypi.org downloads, make these changes to the boot and rootfs partitions to enable headless access :-

#### Enable SSH
sudo touch mountdir/boot/ssh

#### Configure Wifi(s)
sudo nano mountdir/rootfs/etc/wpa_supplicant/wpa_supplicant.conf
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

Next insert the SD card and boot the Pi. Once it's up and running :-
#### Locate using avahi
ping raspberrypi.local

#### Secure shell
> ssh pi@ raspberrypi.local

#### Use raspi-config 
sudo raspi-config
* hostname
* Camera
* gpu
* Expand filesystem

