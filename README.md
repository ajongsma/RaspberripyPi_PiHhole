# Raspberri pi - PiHole edition

# Download Etcher or Apple-Pi-Baker to Flash OS images to SD card(s)
##### https://etcher.io / https://www.tweaking4all.com/hardware/raspberry-pi/macosx-apple-pi-baker/

# Download Raspbian Stretch Lite image
##### https://www.raspberrypi.org/downloads/raspbian/

# Terminal
## Login:
##### $ UserID: pi
##### $ Password: raspberry

## sudo raspi-config
##### $ sudo raspi-config
##### > Interface Options > SSH > Yes
##### > Network Options > Wi-fi
##### > Boot Options -> B1 Desktop / CLI -> B2 Console Autologin
##### > Advanced Options -> A3 Memory Split -> Enter 16

# Terminal / SSH
## Upgrade installed packages
##### $ sudo apt-get update 
##### $ sudo apt-get upgrade
##### $ sudo apt-get autoremove
##### $ sudo apt-get autoclean

## Install Pi-Hole
##### $ curl -sSL https://install.pi-hole.net | bash

## Change Password Pi-Hole web admin interface 
##### $ pihole -a -p

## Pi-hole
##### open https://pi-hole.net

## Pi-hole as All-Around DNS Solution
##### https://docs.pi-hole.net/guides/unbound/

# Other / Notes
###### https://blog.sleeplessbeastie.eu/2018/01/11/how-to-install-and-configure-pi-hole/
###### https://itchy.nl/raspberry-pi-3-with-openvpn-pihole-dnscrypt
###### https://www.ct.nl/achtergrond/versleutelde-dns-requests-met-pi-hole/
