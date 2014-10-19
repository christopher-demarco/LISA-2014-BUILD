# LISA-2014-BUILD


This repository holds all code, config, docs, and resources for the compute side of LISA-2014-BUILD. I suppose there could be some networking stuff here, but that's out of my realm.

I expect we'll use s3 buckets (or bts!?) to store data.

So I guess here's how it goes:
Standard DHCP, BIND cookbooks.

## Roles:
	- lisa (common stuff)
	- dhcp
	- resolv
	- auth
	- mon

Figure out how to use AWS templates to provision nodes.
Then move on to the Nagios, Splunk integrations—deploy and provision based on node inventory.

A major question in my mind is *where* all this documentation/design takes place—slack, Google Docs, in-place (github)? (Those are in decreasing order of abstraction, and inversely Emacs-friendliness :-/ )


- Each templated file should carry a header showing how (or where to learn how) to edit it.

