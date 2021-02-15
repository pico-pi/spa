After creating the :floppy_disk: SD image from www.raspberrypi.org downloads, make these changes to the boot and rootfs partitions to enable headless access :-

#### Enable SSH
>sudo touch mountdir/boot/ssh

#### Configure Wifi(s)
>sudo nano mountdir/rootfs/etc/wpa_supplicant/wpa_supplicant.conf
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

Next insert the SD card and boot the Pi. Once it's up and running, locate using avahi "local" or "home" service
>ping raspberrypi.local

#### Secure shell into the Pi
>ssh pi@ raspberrypi.local

#### Basic system configuration 
>sudo raspi-config
* Change hostname
* Enable camera
* GPU memory split allocate 64MB
* Expand filesystem on reboot

#### Add new user and remove pi account 
>sudo adduser donald

>sudo usermod -a -G adm,dialout,cdrom,sudo,audio,video,plugdev,games,users,input,netdev,gpio,i2c,spi donald

Logout and then log back in with new account

>sudo deluser -remove-home pi


#### key based SSH authentication
On the PC
>ssh-keygen

>ssh-copy-id donald@hostname.local

Now you should be able to login without a password

>ssh donald@hostname.local

Disable password logins

>sudo nano /etc/ssh/sshd_config
```
..
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
..
```

#### Remove bloat
>sudo apt-get remove -purge

