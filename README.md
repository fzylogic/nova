Description
===========

Installs the Openstack compute service (codename: nova) from packages.

http://nova.openstack.org

Requirements
============

Chef 0.10.0 or higher required (for Chef environment use).

Platforms
--------

* Ubuntu-12.04
* Fedora-17

Cookbooks
---------

The following cookbooks are dependencies:

* apt
* database
* glance
* keystone
* mysql
* openssh
* rabbitmq

Resources/Providers
===================

None


Recipes
=======

api-ec2
----
-includes recipe `nova-common`  
-installs AWS EC2 compatible  API and configures the service and endpoints in keystone

api-metadata
----
-includes recipe `nova-common`  
-Installs the nova metadata package

api-os-compute
----
-includes recipe `nova-common`  
-installs OS API and configures the service and endpoints in keystone

api-os-volume
----
-includes recipe `nova-common`  
-installs the OpenStack volume service API

apt
----
-performs an apt-get update  

compute
----
-includes recipes `nova-common`, `api-metadata`, `network`  
-installs nova-compute service

libvirt
----
-installs libvirt, used by nova compute for management of the virtual machine environment  

network
----
-includes recipe `nova-common`  
-installs nova network service

nova-common
----
-Builds the basic nova.conf config file with details of the rabbitmq, mysql, glance and keystone servers. Also builds a .novarc file for root with appropriate environment variables to interact with the nova client cli.

nova-setup
----
-includes recipes `nova-common`, `mysql:client`  
-sets up the nova database on the mysql server, including the initial schema and subsequent creation of the appropriate networks

scheduler
----
-includes recipe `nova-common`  
-nstalls nova scheduler service

vncproxy
----
-includes recipe `nova-common`
-installs and configures the vncproxy service for console access to vms

volume
----
-includes recipes `nova-common`, `api-os-volume`
-installs nova volume service and configures the service and endpoints in keystone 


Attributes 
==========

`nova["db"]` - name of nova database  
`nova["db_user"]` - username for nova database access  
`nova["db_passwd"]` - password for nova database access  
`nova["db_ipaddress"]` - ip address for nova api to bind to

`nova["service_tenant_name"]` - tenant name used by nova when interacting with keystone  
`nova["service_user"]` - user name used by nova when interacting with keystone  
`nova["service_pass"]` - user password used by nova when interacting with keystone  
`nova["service_role"]` - user role used by nova when interacting with keystone  

`nova["compute"]["adminURL"]` - defines the url used to access the OS API for admin functions  
`nova["compute"]["internalURL"]` - defines the url used to access the OS API for user functions from an internal network 
`nova["compute"]["publicURL"]` - defines the url used to access the OS API for user functions from an external network  
`nova["ec2"]["adminURL"]` - defines the url used to access the AWS EC2 compatible API for admin functions  
`nova["ec2"]["internalURL"]` - defines the url used to access the AWS EC2 compatible API for user functions from an internal network  
`nova["ec2"]["publicURL"]` - defines the url used to access the AWS EC2 compatible API for user functions from an external network  

`volume["api_port"]` - port on which nova volumes api runs  
`volume["ipaddress"]` - ip address where nova volumes api runs  
`volume["adminURL"]` - the url used to access the nova volumes API for admin functions  
`volume["internalURL"]` - the url used to access the nova volumes API for user functions from an internal network  
`volume["publicURL"]` - the url used to access the nova volumes API for user functions from an external network  

`public["label"]` - network label to be assigned to the public network on creation  
`public["ipv4_cidr"]` - network to be created (in cidr notation eg 192.168.100.0/24)  
`public["num_networks"]` - number of networks to be created  
`public["network_size"]` - number of IP addresses to be used in this network  
`public["bridge"]` - bridge to be created for accessing the vm network (eg br100)  
`public["bridge_dev"]` - physical device on which the bridge device should be attached (eg eth2)  
`public["dns1"]` - dns server 1  
`public["dns2"]` - dns server 2  

`private["label"]` - network label to be assigned to the private network on creation  
`private["ipv4_cidr"]` - network to be created (in cidr notation eg 192.168.200.0/24)  
`private["num_networks"]` - number of networks to be created  
`private["network_size"]` - number of IP addresses to be used in this network  
`private["bridge"]` - bridge to be created for accessing the vm network (eg br200)  
`private["bridge_dev"]` - physical device on which the bridge device should be attached (eg eth3)  

`virt_type` - what hypervisor software layer to use with libvirt (eg kvm, qemu)  

`libvirt["auth_tcp"]` - the type of authentication your libvirt layer requires  
`libvirt["ssh"]["private_key"]` - private key to use if using ssh authentication to your libvirt layer  
`libvirt["ssh"]["public_key"]` - public key to use if using ssh authentication to your libvirt layer  

Templates
=====
`api-paste.ini.erb` - paste config for nova api middleware  
`libvirt-bin.erb` - initscript for starting libvirtd  
`libvirtd-ssh-config` - config file for libvirt ssh auth  
`libvirtd-ssh-private-key.erb` - private ssh key for libvirt ssh    
`libvirtd-ssh-public-key.erb` - public ssh key for libvirt ssh auth  
`libvirtd.conf.erb` - libvirt config file  
`local_settings.py.erb` - dashboard (horizon) config file  
`mysql-server.seed.erb` - debian preseed file for configuring mysql  
`nova-mysql.cnf.erb` - mysql config file  
`nova.conf.erb` - basic nova.conf file  
`novarc.erb` - contains environment variable settings to enable easy use of the nova client


License and Author
==================

Author:: Justin Shepherd (<justin.shepherd@rackspace.com>)  
Author:: Jason Cannavale (<jason.cannavale@rackspace.com>)  
Author:: Ron Pedde (<ron.pedde@rackspace.com>)  
Author:: Joseph Breu (<joseph.breu@rackspace.com>)  
Author:: William Kelly (<william.kelly@rackspace.com>)  
Author:: Darren Birkett (<darren.birkett@rackspace.co.uk>)  
Author:: Evan Callicoat (<evan.callicoat@rackspace.com>)  

Copyright 2012, Rackspace, Inc.  

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
