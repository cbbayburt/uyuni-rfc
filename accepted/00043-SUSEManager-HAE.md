- Feature Name: SUSE_Manager_on_HAE
- Start Date: 2018-02-23
- RFC PR: #66

# Summary
[summary]: #summary

Configure HAE to run SUSE Manager.

# Motivation
[motivation]: #motivation

For many customers SUSE Manager is a very important part in the total process of patching and installing systems. Often SUSE Manager is also used as the central planning tool.
Not having this tool available could affect daily business activities.
To prevent this customers would like to have SUSE Manager running on SLES High-Availabiliy extension. The ensures that the system is more available.

# Detailed design
[design]: #detailed-design

SUSE Manager will be installed on a two-node cluster running on SLES12 Service Pack 3.
The plan is that this will be an active-passive cluster. All SUSE Manager services will run on 1 of the 2 nodes at any given point in time.

There are 2 additional IP addresses needed.
- admin IP for cluster
- IP for SUSE Manager

The needed certificates should be created before the installation and not generated by SUSE Manager during setup. A procedure to create such a certificate will be included. 
 
The filesystems can be either shared storage (SAN, iSCSI).

The biggest challange is to ensure that all needed directories and files are part of the cluster solution and are available when SUSE Manager is loaded on the other node. Some more research is needed and the needed steps/directories will be included in the documentation. Currently the following have been identified:

- /var/spacewalk 
- /var/lib/pgsql
- /var/cache/rhn
- /var/cache/salt
- /srv
- /var/lib/spacewalk
- /var/lib/cobbler
- /var/lib/rhn
- /var/lib/jabberd
- /var/lib/salt
- /var/lib/xen/images
- /var/lib/libvirt/images
- /etc/sysconfig/rhn
- /etc/rhn
- /etc/salt
- /etc/tomcat
- /usr/share/susemanager
- /usr/share/rhn
- /var/log/apache2
- /var/log/tomcat
- /var/log/cobbler
- /var/log/atftpd
- /var/log/spacewalk
- /var/log/salt
- /var/log/rhn

# Drawbacks
[drawbacks]: #drawbacks

It is adding an additional layer of complexity. When researching an issue, both nodes need to be included.

# Alternatives
[alternatives]: #alternatives

None.

# Unresolved questions
[unresolved]: #unresolved-questions

What to do about licensing? SUSE Manager will be installed on 2 server. Does the customer need 2 licenses for SUSE Manager or only 1 as this is running as 1 SUSE Manager.
