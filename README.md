# Raspberry Pi - PiHole edition

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

## Upgrade firmware
##### $ sudo raspi-config
##### $ sudo rpi-update

# Terminal / SSH
## Upgrade packages and distribution
##### $ sudo apt-get update && sudo apt-get upgrade
##### $ sudo apt-get dist-upgrade

## Cleanup & Install extra tools
##### $ sudo apt-get install -y autoremove autoclean sysstat vnstat screen

## Enable NTP time
##### $ timedatectl set-ntp true 
##### $ timedatectl status

## Install Pi-Hole
##### $ curl -sSL https://install.pi-hole.net | bash

## Change Password Pi-Hole web admin interface 
##### $ pihole -a -p

## Update Pi-Hole
##### $ pihole -up

## Pi-hole
##### open https://pi-hole.net


## Enable password-less login
##### Create the .ssh directory via install -d -m 700 ~/.ssh
##### Create a SSH key on your PC: ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
##### Install your public key for user 'pi' cat ~/.ssh/id_rsa.pub | ssh pi@IPADDRESS 'cat >> .ssh/authorized_keys'
##### Install your public key for user 'root' cat ~/.ssh/id_rsa.pub | ssh root@IPADDRESS 'cat >> .ssh/authorized_keys'

## Add Whitelist
#### https://github.com/anudeepND/whitelist



# Testing
## Add local DNS resolution
#### Create a second dnsmasq config file:
```
echo "addn-hosts=/etc/pihole/lan.list" | sudo tee /etc/dnsmasq.d/02-lan.conf
```
#### Create a hosts file for your network at /etc/pihole/lan.list with the format ipaddress fqdn hostname (tabbed between each). For example
```
192.168.1.1    UbiquitiGateway.local    UbiquitiGateway
```

# Add Customs
## Extra blocklists
```
pihole tee -a /etc/pihole/adlists.list >/dev/null << EOF
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts 
https://mirror1.malwaredomains.com/files/justdomains 
http://sysctl.org/cameleon/hosts 
https://zeustracker.abuse.ch/blocklist.php?download=domainblocklist 
https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt 
https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt 
https://hosts-file.net/ad_servers.txt 
https://hosts-file.net/exp.txt 
https://hosts-file.net/emd.txt 
https://hosts-file.net/psh.txt 
https://v.firebog.net/hosts/Airelle-hrsk.txt 
https://v.firebog.net/hosts/Shalla-mal.txt 
https://ransomwaretracker.abuse.ch/downloads/RW_DOMBL.txt 
https://ransomwaretracker.abuse.ch/downloads/LY_C2_DOMBL.txt 
https://ransomwaretracker.abuse.ch/downloads/CW_C2_DOMBL.txt 
https://ransomwaretracker.abuse.ch/downloads/TC_C2_DOMBL.txt 
https://ransomwaretracker.abuse.ch/downloads/TL_C2_DOMBL.txt 
http://www.networksec.org/grabbho/block.txt 
https://isc.sans.edu/feeds/suspiciousdomains_Medium.txt 
http://someonewhocares.org/hosts/hosts 
https://s3.amazonaws.com/lists.disconnect.me/simple_malvertising.txt 
http://www.joewein.net/dl/bl/dom-bl.txt
https://raw.githubusercontent.com/crazy-max/WindowsSpyBlocker/master/data/hosts/spy.txt 
https://v.firebog.net/hosts/static/SamsungSmart.txt 
https://gist.githubusercontent.com/anudeepND/adac7982307fec6ee23605e281a57f1a/raw/5b8582b906a9497624c3f3187a49ebc23a9cf2fb/Test.txt 
https://raw.githubusercontent.com/StevenBlack/hosts/master/data/KADhosts/hosts 
https://reddestdream.github.io/Projects/MinimalHosts/etc/MinimalHostsBlocker/minimalhosts 
https://raw.githubusercontent.com/StevenBlack/hosts/master/data/add.Spam/hosts 
https://v.firebog.net/hosts/static/w3kbl.txt
EOF
```

## Manually Whitelisted Domains
```
pihole -w pubsub.plex.tv plugins.plex.tv chapterdb.plex.tv cloudfront.net \
plex.direct csi.gstatic.com dl.opensubtitles.org speedvideo.net ton.twimg.com \
twimg.com chapterdb.plex.tv tinyurl.com bit.ly ton.twimg.com dropbox.com \
pubsub.plex.bz fonts.gstatic.com www.googletagmanager.com \
links.services.disqus.com ump.plex.tv meta.plex.tv goo.gl
```

## Manually Blacklisted Domains
```
pihole -b dxp.baidu.com hmma.baidu.com pasta.esfile.duapps.com \
neweegg.net config.a-mo.net nrc.tapas.net xpu.samsungelectronics.com \
upu.samsungelectronics.com dns.msftncsi.com bn2wns1b.wns.windows.com \
a-0001.a-msedge.net msnbot-65-52-108-90.search.msn.com a-0011.a-msedge.net \
bn2ap002.device.ra.live.com a.ads1.msn.com a.ads2.msn.com ad.doubleclick.net \
adnexus.net adnxs.com ads.msn.com ads1.msads.net ads1.msn.com \
az361816.vo.msecnd.net az512334.vo.msecnd.net ca.telemetry.microsoft.com \
cache.datamart.windows.com choice.microsoft.com corp.sts.microsoft.com \
choice.microsoft.com.nsatc.net choice.microsoft.com.nstac.net \
choice.microsoft.com.nstac.net compatexchange.cloudapp.net corp.sts.microsoft.com \
corpext.msitadfs.glbdns2.microsoft.com cs1.wpc.v0cdn.net \
db3wns2011111.wns.windows.com df.telemetry.microsoft.com \
diagnostics.support.microsoft.com fe2.update.microsoft.com.akadns.net \
fe3.delivery.dsp.mp.microsoft.com.nsatc.net feedback.microsoft-hohm.com \
feedback.search.microsoft.com feedback.windows.com i1.services.social.microsoft.com \
i1.services.social.microsoft.com.nsatc.net msnbot-207-46-194-33.search.msn.com \
oca.telemetry.microsoft.com oca.telemetry.microsoft.com.nsatc.net \
pre.footprintpredict.com preview.msn.com rad.msn.com \
redir.metaservices.microsoft.com reports.wes.df.telemetry.microsoft.com \
settings-sandbox.data.microsoft.com settings-win.data.microsoft.com \
settings.data.microsof.com sls.update.microsoft.com.akadns.net spynet2.microsoft.com \
spynetalt.microsoft.com sqm.df.telemetry.microsoft.com sqm.telemetry.microsoft.com \
sqm.telemetry.microsoft.com.nsatc.net ssw.live.com statsfe1.ws.microsoft.com \
statsfe2.update.microsoft.com.akadns.net statsfe2.ws.microsoft.com \
survey.watson.microsoft.com telecommand.telemetry.microsoft.com \
telecommand.telemetry.microsoft.com.nsatc.net telemetry.appex.bing.net \
telemetry.microsoft.com telemetry.urs.microsoft.com view.atdmt.com \
v10.vortex-win.data.microsoft.com vortex-sandbox.data.microsoft.com \
vortex-win.data.microsoft.com vortex.data.microsoft.com watson.live.com \
watson.microsoft.com watson.ppe.telemetry.microsoft.com \
watson.telemetry.microsoft.com watson.telemetry.microsoft.com.nsatc.net \
wes.df.telemetry.microsoft.com win10.ipv6.microsoft.com adservice.google.com \
ads.aws.viber.com stats.appsflyer.com adservice.google.ie referrer.disqus.com \
browser.pipe.aria.microsoft.com tracking.campaign-tracking-service.placelocal.com \
primoitaliablob.blob.core.windows.net srv.dc-1.net \
wdcpeurope.microsoft.akadns.net wdcp.microsoft.akadns.net
```






## Pi-hole as All-Around DNS Solution
##### https://docs.pi-hole.net/guides/unbound/

# Other / Notes
###### https://blog.sleeplessbeastie.eu/2018/01/11/how-to-install-and-configure-pi-hole/
###### https://itchy.nl/raspberry-pi-3-with-openvpn-pihole-dnscrypt
###### https://www.ct.nl/achtergrond/versleutelde-dns-requests-met-pi-hole/
###### https://github.com/magicdude4eva/PiHoleCloudFlareD
###### https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=23440&sid=7e9b82328ff4a5ef30f2a867cdf25bd5
