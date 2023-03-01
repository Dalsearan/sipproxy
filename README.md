# sipproxy

This is project for proxy (sip and rtp) calls.

kamailio config for https://hub.docker.com/repository/docker/dalsearan/proxy_for_sip/general

# Minimum server requirements:
* Debian 10/11
* At least 10 GB of free disk space
* 1 GB of RAM
* Public static ip-address
* Installed git

# Installation instructions:

1. Clone this repo to a local VDS/VPS:

       # git clone https://github.com/Dalsearan/sipproxy.git

2. Go to the sipproxy directory:

       # cd sipproxy

3. Run command to make executable:

       # chmod +x setup-sipproxy.x

4. Then run as a root on Debian system:

       # ./setup-sipproxy.x
  
5. Follow the installation instructions.


# Or you can use a one-line command:

    # apt update && apt -y install git && git clone https://github.com/Dalsearan/sipproxy.git && cd sipproxy && chmod +x setup-sipproxy.x && ./setup-sipproxy.x
  
  
# Using of sipproxy:

## SIP phone:
   Set the ip-address and port ***25060*** of sipproxy as an outbound proxy in your SIP phone settings.
  
## Asterisk:
  
 ###  SIP:
 Set the parameter "outboundproxy=ip-address of sipproxy:25060" for the SIP-trunk in sip.conf, for example:
 
    outboundproxy=192.168.0.1:25060
    
 ###  PJSIP:
 https://wiki.asterisk.org/wiki/display/AST/PJSIP+with+Proxies
   
##  FreeSwitch:
  
   In a SIP trunk parameter file such as "sip-trunk.xml", add the following parameter <param name="outbound-proxy" value="ip-address of sipproxy"/>, for example:
   
    <include>
      <!--gateway name required, you will use this in the outbound dialplan -->
        <gateway name="sip-trunk">
          ...
          <param name="outbound-proxy" value="192.168.0.1:25060"/>
          ...
        </gateway>
    </include>
