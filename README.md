## A Light Script For You To Setup Shadowsocks-libev Server with High-Speed Connections and Newest Powerful Features

## Twist Features
- **Fast, Secured and Stable Connections by Shadowsocks**
- **Multithreading** Support
- **TCP Fast Open** Support
- **Simple Obfs** Support
- **IPv4 & IPv6** Support
- **Optimised Performance** Using Google BBR TCP Controler and Support UDP Transfer
- **High Security** Support AEAD Cipher & Encryption
- **Newest Features** Support TLS Obfs & Obfs URI in simple-obfs
- **Fine Compatibility** Support Various Shadowsocks Based Clients
- **One-key Installation** and QRCode Scan to Connect on Your Devices
- **SS Scheme & QRCode** Basic Connect Information Auto Generate and Shows Full Connect Information
- **Highly Concealed** It is able to Fake as a Web Server Using Apache and Enabled Fail2ban to Ban Force Crackers

## Server Requirements
- Ubuntu 18.04(Bionic), 17.10(Artful), 17.04(Zesty), 16.10(Yakkety), 16.04(Xenial)
- Debian 9(Stretch), 8(Jessie) 
- Cent OS 7, 6
- Red Hat 7, 6
- Fedora 26, 25
- Arch Linux
- Raspbian

## Set Up your Shadowsocks-libev Server
Please **Run Command** below on your server to **Install Twist**
```bash
sudo wget https://raw.githubusercontent.com/Unbinilium/Twist/master/twist -O twist.sh && sudo chmod -x twist.sh && sudo bash twist.sh
```

## Attention
- Please make sure that your server was able to **Connect to the Internet and Opened these Inboard & Outboard Ports** below. It required by shadowsocks-libev service and apache fake service based on your configurations. And It will be automatically configured on your System Side but will not be on the Server Management Console. You may manually open these port
```txt
UDP 443
TCP 80
TCP 443
```
- Twist will make changes to your Server, so it is necessary to backup your files that stored on the Server. And Twist will automatically backup files what it makes changes to while Install and restore them while Uninstall. The default back path is listed here
```txt
/etc/twist
```
- The simple **log** is stored at ```/var/log/twist```. It only recored Twist service status, not the verbose log. If you want know more details about shadowsocks-libev server, try this command ```ss-server``` or even more detailed logs using ```systemctl status shadowsocks-libev-server``` if you are using **systemd** to manage its service. Also check the **syslog** using command ```cat /var/log/syslog``` when this shadowsocks-libev feature called **use_syslog** is on

## Custom
Change the default configurations by editing Twish before install, the manual and detailed information of shadowsocks-libev configurations is at <a href="https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File" target="_blank">shadowsocks-libev Wiki</a>
```bash
sudo nano twist.sh # Edit the value below on 'function *config'
```
If you have already installed Twist, try this by editing raw config file that installed on your server instead of the install script 
```bash
sudo twist custom  # Edit the value in json format
```
Edit values in typename="**HERE**", save and run Twist after you have confirmed that it is correct
```txt
 PORT="443"                       # Server port
 PASSWORD=""                      # Password used for encryption, auto generate if left free
 METHOD="xchacha20-ietf-poly1305" # Encryption, AEAD is better than OTA cipher which is already departed
 TIMEOUT="600"                    # Drop connections if it not using in seconds
 OBFS="tls"                       # Obfs method using tls or http
 OBFSHOST="mzstatic.com"          # Obfs host address
 OBFSURI="/"                      # Obfs specify the client request path uri
 FASTOPEN="true"                  # Use TCP fastopen that reduces TCP handshake time
 REUSEPORT="true"                 # Use TCP port reuse
 DNS1="8.8.8.8"                   # Default DNSv4 server address 1 from Google Public DNS
 DNS2="8.8.4.4"                   # Default DNSv4 server address 2 from Google Public DNS
 DNSv6a="2001:4860:4860::8888"    # Default DNSv6 server address a from Google Public DNSv6
 DNSv6b="2001:4860:4860::8844"    # Default DNSv6 server address b from Google Public DNSv6
 DSCP="EF"                        # Default dscp using expedited forwarding
 MODE="tcp_and_udp"               # Allow both connection use TCP and UDP
 MTU=""                           # Default mtu size, leave it blank to auto detect
 MPTCP="false"                    # Use multi-TCP experimental feature
 IPV6FIRST="false"                # Use IPv6 default when available, auto off if no IPv6 address detected
 SYSLOG="true"                    # Export verbose log to /var/log/syslog
 NODELAY="true"                   # Reduce the TCP respond time delay
 FWS="enable"                     # Fake as a apache web server for concealing
 BBR="enable"                     # Use Google BBR for low delay network to get faster speed
```
You could also install any version of shadowsocks-libev and its components that you want. Do this by changing these and following its formart.
```txt
 libsodiumver=""                  # The libsodium version formart *.*.*
 mbedtlsver=""                    # The mbedtls version formart *.*.*
 sslibevtag=""                    # The shadowsocks-libev version formart v*.*.*
 ssobfstag=""                     # The simple-obfs version formart v*.*
```
If you leave it blank, Twist will automaticly find the newest released version to install. And If you customed these version, make sure that each version has good compatibility with your system and each components could work well together

## Encrypt Method Cipher
- There are some **recommend AEAD Ciphers** to use if the default cipher is not available for the clients on your device
```txt
aes-128-gcm
aes-192-gcm
aes-256-gcm
chacha20-ietf-poly1305
xchacha20-ietf-poly1305
```
- Also the Stream Ciphers listed here, which are not recommend. If there is no other choice, please try these
```txt
rc4
rc4-md5
rc2-cfb
bf-cfb
des-cfb
idea-cfb
seed-cfb
cast5-cfb
camellia-128-cfb
camellia-192-cfb
camellia-256-cfb
aes-128-cfb
aes-192-cfb
aes-256-cfb
aes-128-ctr
aes-192-ctr
aes-256-ctr
salsa20
chacha20
chacha20-ietf
```

## Simple Obfs
Here is the deafult configurations of simple-obfs, it will not be run without configure it on your clients side. And you could use shadowsocks without set up simple-obfs on your clients. If you used the URLSchemes or QRCode to setup your clients, simple-obfs may not be configured in some old clients or third-part clients
```txt
OBFS="tls"
OBFSHOST="mzstatic.com"
OBFSURI="/"
```

## Check and Change Shadowsocks-libev Status
- Check if shadowsocks-libev is running on your server
```bash
twist status        # Check Shadowsocks Status
```
- Change the status of shadowsocks-libev by these commands
```bash
sudo twist start    # Start Shadowsocks Service
sudo twist stop     # Stop Shadowsocks Service
sudo twist restart  # Restart Shadowsocks Service
```

## Setup Shadowsocks-libev to Connect to the Server on your Devices
It requires shadowsocks based clients on your device and you may have to manually set up some features or you can use the URLScheme and QRCode for configuration. Be careful and make sure there is a simple-obfs plugin on your client side if you used this feature. Otherwise, if the default cipher is not available on your clients, try other cipher I have mentioned yet. Don't dismiss any useful information for troubleshooting

## Update Twist
Please **Run Command** to update Twist
```bash
sudo twist update
```
You can also update Twist automaticly by using ```crond``` Service
```bash
echo "0 0 1 * * root bash /usr/bin/twist update" >> /etc/crontab && crontab -u root /etc/crontab
```
The commands means **Twist will automaticly check updates on the first day of every month**


## Uninstall Twist
Please **Run Command** to uninstall Twist
```bash
sudo twist uninstall
```

## Author & Acknowledge
<a href="https://github.com/Unbinilium" target="_blank">Unbinilium</a> -- This script is mainly using <a href="https://github.com/shadowsocks" target="_blank">Shadowsocks</a>
