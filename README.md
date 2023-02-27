# sipproxy

This is project for proxy (sip and rtp) calls.

kamailio config for https://hub.docker.com/repository/docker/dalsearan/proxy_for_sip/general

Minimum server requirements:
* Debian 10/11
* At least 10 GB of free disk space
* 1 GB of RAM
* Public static ip-address
* Installed git

To install sipproxy:
1. Clone this repo to a local VDS/VPS:

  ~# git clone https://github.com/Dalsearan/sipproxy.git

2. Go to the directory sipproxy:

  ~# cd sipproxy

3. Execute:

  ~# chmod +x setup-sipproxy.x

4. Run as a root on Debian system:

  ~# ./setup-sipproxy.x
  
5. Follow the installation instructions.


Or you can use a one-line command:

  ~# apt update && apt -y install git && git clone https://github.com/Dalsearan/sipproxy.git && cd sipproxy && chmod +x setup-sipproxy.x && ./setup-sipproxy.x
