<!-- permalink: aaba071ba66b59be6fda5443994844f8 DO NOT DELETE OR EDIT THIS LINE -->
# Alpine Podman and Security Setup

* `apk add nano`
* `export EDITOR='nano'`


* `apk add podman`
* `rc-update add cgroups`
* `rc-service cgroups start`

* `nano .profile`


```
export EDITOR="nano"

alias docker="podman"
alias dc="docker compose"

alias gs="git status"
alias gc="git commit -m"
alias ga="git add"
```


* `addgroup sudo`
* `visudo` # enable sudo group

* `adduser [user-no-brackets]`
* `adduser [user-no-brackets] sudo`


* ~~#modprobe tun~~
* ~~#echo tun >>/etc/modules~~ - appears unecessary
* `echo [user-no-brackets]:100000:65536 >/etc/subuid`
* `echo [user-no-brackets]:100000:65536 >/etc/subgid`

* `podman run --rm hello-world` # as [user-no-brackets] to test rootless permissions

* `setup-timezone`

* `crontab -e`


```
* * * * * /usr/bin/uptime >> ~/load
* * * * * /usr/bin/free -h >> ~/load
```


* `sudo apk update`
* `sudo apk add py3-pip`

* `python3 -m venv .`
* `source bin/activate` #(from venv dir)
* `pip3 install podman-compose`

* `sudo ln /usr/bin/podman /usr/bin/docker`

* `echo "net.ipv4.ip_unprivileged_port_start = 80" >> /etc/sysctl.conf`
