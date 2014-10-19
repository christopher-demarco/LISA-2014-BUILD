# LISA-2014-BUILD

This is a sketch of how this beast might look. This is not one monolithic repo because apparently that's an antipattern.

I suppose there could be some networking stuff here, but that's out of my realm.

I expect we'll use s3 buckets (or bts!?) to store data.

Each templated file should carry a header showing how (or where to learn how) to edit it... (This raises the nagging question of whether everybody knows/is cool with Chef)

## Cookbooks
	* users
	* environment (editors, colordiff, et al.)
	* bind
	* mon-client
	    * nagios-plugins
		* munin-client
		* logdest
	* mail
	* bind
	* dhcpd
	* tftpd
	* nagios-server (stuff like this can config based on node inventory)
	* munin-server
	* splunk-server

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



