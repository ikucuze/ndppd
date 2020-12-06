# NDPPD

***ndppd***, or ***NDP Proxy Daemon***, is a daemon that proxies *neighbor discovery* messages. It listens for *neighbor solicitations* on a
specified interface and responds with *neighbor advertisements* - as described in **RFC 4861** (section 7.2). 

## Current status

Version 0.x has been discontinued, and is being replaced by `1.0-devel` which you can find
[here](https://github.com/DanielAdolfsson/ndppd/tree/1.0-devel).

## Autostartup Setup

To enable autostartup of the compiled **ndppd** please follow the steps below, you will have needed to setup your configuration and compiled this project already. __For this tutorial I have used the directory `/home/ubnt` to store my compiled ndppd and its configuration.__ **Change these to your liking.**

#### 1 Create and chmod the startup scripts.
```bash
sudo touch /config/scripts/post-config.d/ipv6.sh && sudo touch /config/scripts/daemon.sh
sudo chmod 755 /config/scripts/post-config.d/ipv6.sh && sudo chmod 755 /config/scripts/daemon.sh
```

#### 2 Now popullate the files with this startup code.
- Change the ndppd directories used to where you saved yours, same with the configuration file.
- Make sure that if you are using an editor on windows over SFTP to popullate these files that EOL Conversion is set to Unix (LF).
##### `/config/scripts/post-config.d/ipv6.sh`
```bash
#!/bin/bash
nohup /config/scripts/ipv6.sh & 
```
##### `/config/scripts/daemon.sh`
```bash
#!/bin/bash
sudo /home/ubnt/ndppd -c /home/ubnt/ndppd.conf
```

#### 3 Make sure that ndppd is executable too and you're done!
```bash
sudo chmod 755 /home/ubnt/ndppd
```

All you have to do now is reboot the router and everything should be running smoothly.
