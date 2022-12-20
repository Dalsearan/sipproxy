# sipproxy

this is project for proxy (sip and rtp) calls. Project branch differs in:

branch with SIP registration with hidden topology - master branch 

branch with SIP registration as original contact + path header - branch name PATH (TODO)

kamailio config for https://hub.docker.com/repository/docker/dalsearan/proxy_for_sip/tags?page=1&ordering=last_updatedg

docker pull dalsearan/proxy_for_sip:fin

docker run --net=host --cap-add=NET_ADMIN --cap-add=NET_RAW --cap-add SYS_PTRACE --cgroupns=host --privileged -td -v /sys/fs/cgroup:/sys/fs/cgroup:rw --name=sipproxy --hostname=sipproxy dalsearan/proxy_for_sip:fin /sbin/init

sudo docker container exec -it sipproxy /bin/bash

change IP's here: 
/usr/local/kamailio532/etc/kamailio/test_defs.cfg 
and 
/etc/rtpengine/rtpengine.conf