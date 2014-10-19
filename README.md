# LISA-2014-BUILD

Everything is modular: Go look at the other repositories at https://github.com/christopher-demarco

You should be on slack: https://lisa2014-build.slack.com.

Build once, run anywhere.
(where have we heard that before?)
Provision ec2 and vSphere with the same Chef.
Do it again next year with 80% less effort.
I expect we'll use s3 buckets (or bts!?) to store what little actual data there is.


*DOMAIN EXPERT WANTED* Networking—vlans, QoS, etc. 
Somebody out there must grok v6.


Each templated file should carry a header showing how (or where to learn how) to edit it.

Domain experts should be able to (relatively) effortlessly drop in, say specify the version of BIND, chroot it, switch it out for djbdns or...) 

Sysadmin scalability is important. A bus factor of 1 is bad.


*DOMAIN EXPERT WANTED* Security.
Do we need PKI: cert management, single-signon, etc.? 
Do we sign DNS or down that way madness lies?


Design and documentation is paramount.
Breadth-first.


# Cookbooks
These are where you specify how one might configure a particular app.
The details of *which* DHCP address range, of *to whom* a syslog daemon might send remote logs—these are data, not specified here.

## Common
users (ssh keys in encrypted databags, groups, homedirs, dotfiles, etc.)
userland  (emacs/vi, colordiff, tcpdump, netcat, et al.)
mail (somebody please make it simple)

## DNS
bind https://supermarket.getchef.com/cookbooks/bind
General package installation. Selection of subsystems.
In theory, it should be possible to run both auth and resolv

auth is a special case of bind. Take DHCP updates, push to secondaries.
Should this be mostly-config, i.e. attributes?

resolv is a special case of bind. See ``auth'', above. 

## DHCP gets tricky because there are multiple nets.


## bootstrap
dhcpd
tftpd

### nagios (or Zenoss?)
nagios
nagios-server (stuff like this can config based on node inventory)
nagios-client

splunk
syslog-client

munin https://supermarket.getchef.com/cookbooks/munin
munin-server 
munin-client 

## Roles:
    * lisa (common stuff)
	    * munin-node
		* loghost
	* dhcp
	* resolv
    * auth
    * mon
	* tester
	* build
	
## Environments (associate with cookbook tags)
	* dev
	* prod
	
## Data bags
	* users

Figure out how to use AWS templates to provision nodes.



