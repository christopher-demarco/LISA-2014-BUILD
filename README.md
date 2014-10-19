# LISA-2014-BUILD

You should be on slack: https://lisa2014-build.slack.com


All Chef stuff is modular: Go look at the other Chef repositories at https://github.com/christopher-demarco.


Build once, run anywhere. (where have we heard that before?)
Provision ec2 and ESXi with the same Chef.
Do it again next year with 80% less effort.

The point of Chef is to reduce complexity, not increase it. If domain experts have to jump through hoops, if only one person can maintain it, that's a problem. Sysadmin scalability is important. A bus factor of 1 is bad..

Domain experts should be able to (relatively) effortlessly drop in, say specify the version of BIND, chroot it, switch it out for djbdns or...) 
Each templated file should carry a header showing how (or where to learn how) to edit it.

Chef shouldn't be friction, it should be empowerment.


*DOMAIN EXPERT WANTED* Networking—vlans, QoS, etc. 
Somebody out there must grok v6.


*DOMAIN EXPERT WANTED* Security.
Do we need PKI: cert management, single-signon, etc.? 
Do we sign DNS or down that way madness lies?


Design and documentation is paramount.
Breadth-first.


# Scalability
DHCP is gonna suck, we have to balance lease renewal traffic with address space etc.
Lease activity can inform INFOSEC.

DNS could be worse.
Unless we advert 8.8.8.8 to usernet, and only recurse for ourselves?
Or do we eschew caching recursive resolution altogether?

# Deployment
Whether to schedule chef-client in cron, to only do it by hand, or what?


# Cookbooks

TODO: So there needs to be an easy way to get all this stuff checked out into one place so you can hack on it. SOMEBODY (and not just me) needs to be able to maintain it—knife-uploading them to chef-server, re-running the client on nodes)

TODO: Berksfile vs. chef-librarian? Again, how does a dev provision the environment? Cookbooks are uploaded to chef-server, but how to manage 'em on one's workstation?

## Common
users (ssh keys in encrypted databags, groups, homedirs, dotfiles, etc.)

userland  (emacs/vi, colordiff, tcpdump, netcat, et al.)

mail (somebody please make it simple)
https://supermarket.getchef.com/cookbooks/postfix


## DNS

https://supermarket.getchef.com/cookbooks/bind

dns-client (what resolvers to use)

dns https://supermarket.getchef.com/cookbooks/bind is the subsystem and its installation.

dns-auth is a special case of bind. Take DHCP updates, push to secondaries.
Should this be mostly-config, i.e. attributes?

resolv is a special case of bind. Cache like hell and try not to crash.


## DHCP 
DHCP gets tricky because there are multiple nets. We have a large address space, which is going to be, uh, interesting for the infosec guys, but freeing leases vs. reducing traffic has to be a consideration.

dhcp-server-role https://github.com/christopher-demarco/lisa2014-dhcp-server-role

dhcp-client: Makes a client get its network information from DHCP, and register hostname in DNS.


## tester
A simulated user, a client of DHCP/DNS etc. Unit testing at layer 8.
Chaos monkey.

## bootstrap
tftp-server for network gear

ubuntu-mirror


### nagios (or Zenoss?)
nagios base package

nagios-server (stuff like this can config based on node inventory. All apps therefore must advertise where they listen, so we can automagically monitor it. Scale, babies.)

nagios-client (this is custom nagios plugins or zenoss agents or whatthefuckever)

*DOMAIN EXPERT WANTED* Splunk 

syslog-client (node search for target)

munin https://supermarket.getchef.com/cookbooks/munin

munin-server 

munin-client 
I've done this and written a few plugins, but it's uninteresting. Happy to let somebody else have a turn on the bicycle.


# Roles:
The "role" a particular node ("machine," could be virtual or physical) plays. Define the recipes that will be applied to any node which receives this role.

Mostly assignment of attributes to things.

TODO: How do you write one of these, and push it up to the server? 

lisa: (probably a bad name) (everything gets this) users, userland, mail, dns-client, 

nagios-client, syslog-client, munin-client

dhcp-server

dns-resolver

dns-auth

splunk-server

nagios-server

tester

build


# Environments
My understanding is that this is primarily a vehicle for tying a level-of-service to a particular git tag. Dev & prod.
	

# Data bags
Where you keep pure data. userids, passwords, keys and certs in encrypted databags; subnet lists, etc.

This is JSON, so we should reference schemata here.



# AWS
Figure out how to use AWS templates to provision VMs for nodes.


# VMWare
Figure out how to provision VMs for nodes.
