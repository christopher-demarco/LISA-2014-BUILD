# LISA-2014-BUILD

Everything is modular: Go look at the other repositories at https://github.com/christopher-demarco

You should be on slack: https://lisa2014-build.slack.com.

Build once, run anywhere.
(where have we heard that before?)
Provision ec2 and vSphere with the same Chef.
Do it again next year with 80% less effort.

Because posterity, design and documentation is paramount.

I suppose there could be some networking stuff here, but that's out of my realm.

I expect we'll use s3 buckets (or bts!?) to store data.

Each templated file should carry a header showing how (or where to learn how) to edit it.

Domain experts should be able to (relatively) effortlessly drop in, say specify the version of BIND, chroot it, switch it out for djbdns or...) 

Sysadmin scalability is important. A bus factor of 1 is bad.

Breadth-first.

# Cookbooks

## Common
users
userland  (editors, colordiff, et al.)
nagios-client (plugins)
munin-client (plugins)
syslog
mail


## DNS
bind https://supermarket.getchef.com/cookbooks/bind
General package installation. Selection of subsystems.
In theory, it should be possible to run both auth and resolv

auth is a special case of bind. Take DHCP updates, push to secondaries.
Should this be mostly-config, i.e. attributes?

resolv is a special case of bind. See ``auth'', above. 

## DHCP


## bootstrap
dhcpd
tftpd

### mon
nagios-server (stuff like this can config based on node inventory)
splunk-server

munin https://supermarket.getchef.com/cookbooks/munin
munin-server
munin-client /supra/

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



