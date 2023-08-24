# sipproxy

this is project for proxy (sip and rtp) calls. Project branch differs in:

branch with SIP registration with hidden topology - master branch 

branch with SIP registration as original contact + path header - branch name PATH (TODO)

kamailio config for https://hub.docker.com/repository/docker/dalsearan/proxy_for_sip/tags?page=1&ordering=last_updatedg

docker pull dalsearan/proxy_for_sip:fin

docker run --net=host --cap-add=NET_ADMIN --cap-add=NET_RAW --cap-add SYS_PTRACE --cgroupns=host --privileged -td -v /sys/fs/cgroup:/sys/fs/cgroup:rw --name=sipproxy --hostname=sipproxy dalsearan/proxy_for_sip:fin /sbin/init

sudo docker container exec -it sipproxy /bin/bash (if container doesnt start -check ***PS at bottom of Readme)

what happens on start inside:
firstly - ipaddress change script:
```
cat /etc/init.d/ipaddress_to_kamailio
#!/bin/bash
EXTIPCHANGE=$(wget -O - -q icanhazip.com)
LOCALIPCHANGE=$(ip -br a | grep UP | awk '{print $3}' | cut -d/ -f1)
cp -f /etc/kamailio/test_defs.cfg /etc/kamailio/test_defs.cfg.tmp && sed -i "s/EXTIPCHANGE/$EXTIPCHANGE/" /etc/kamailio/test_defs.cfg.tmp && sed -i "s/LOCALIPCHANGE/$LOCALIPCHANGE/" /etc/kamailio/test_defs.cfg.tmp && cp -f /etc/kamailio/test_defs.cfg.tmp /etc/kamailio/defs.cfg

cp -f /etc/rtpengine/rtpengine.conf.bak /etc/rtpengine/rtpengine.conf.tmp && sed -i "s/LOCALIPCHANGE/$LOCALIPCHANGE/" /etc/rtpengine/rtpengine.conf.tmp && sed -i "s/EXTIPCHANGE/$EXTIPCHANGE/" /etc/rtpengine/rtpengine.conf.tmp && cp -f /etc/rtpengine/rtpengine.conf.tmp /etc/rtpengine/rtpengine.conf

systemctl stop rtpengine-daemon.service
sleep 2
systemctl start rtpengine-daemon.service
sleep 1
systemctl restart kamailio
```

if something goes wrong - check ip manyally in /etc/kamailio/defs.cfg and /etc/rtpengine/rtpengine.conf

 ***PS
docker container doesnt want to run systemd so if container didn't start - modify /boot/default/grub:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nouveau.modeset=0 systemd.unified_cgroup_hierarchy=false"
```

 update-grub
and restart host machine

