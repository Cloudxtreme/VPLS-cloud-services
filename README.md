VPLS - OpenStack Service Manager
===================

This is a set of scripts and JSON files to manage starting and stopping OpenStack and supporting services and commands. I"ve run into a lot of problem with server shutdowns and restarts, where OpenStack services don"t start up in the correct order causing a break in OpenStack functionality.  

Please note that this package has only been testing on RHEL/CentOS 6.x. You are welcome to try modifying it to support earlier revisions of RHEL/CentOS or other Linux platforms and submit the changes back here.  

Installation
-------------------
Clone the source code to your OpenStack server and make sure the '/etc/osm' directory exists:

    [root@server ~]# git clone https://github.com/djtaylor/VPLS-cloud-services.git  
    [root@server ~]# mkdir -p /etc/osm

Copy the following files to the specified destinations on your CentOS 6.x server:  
    
    [root@server ~]# cp VPLS-cloud-services/bin/osm /usr/bin/osm  
    [root@server ~]# cp VPLS-cloud-services/init.d/osm /etc/init.d/osm  
    [root@server ~]# cp VPLS-cloud-services/json/* /etc/osm/.  

Make sure both "osm" files are executable:  

    [root@server ~]# chmod +x /usr/bin/osm /etc/init.d/osm

Add the "osm" service to using chkconfig:

    [root@server ~]# chkconfig --add osm  

Configuration
-------------------
**Startup/Shutdown Order**  
To set the startup and shutdown order for OpenStack services, edit the "/etc/osm/services.json" file. This file contains a list of OpenStack services (i.e., keystone, nova, cinder, etc.), their startup/shutdown priority, and a list of sub-services (i.e., openstack-nova-api, openstack-nova-compute, etc.).  

    [root@server ~]# vi /etc/osm/services.json  

**OpenStack Service Runlevels**  
This file is a replacement for chkconfig run levels. You MUST disable these services in chkconfig otherwise this script will not work properly. A service in this file can either be set to "on" or "off".  

    [root@server ~]# vi /etc/osm/services.run.json  

**OpenStack Pre-Start/Stop Tasks**  
Depending on the server and your OpenStack environment, you may want to start specific services on specific nodes, and run arbitrary commands prior to startup and shutdown. This file gives you the means to specify pre-start services, and pre-start/stop Linux commands:  

    [root@server ~]# vi /etc/osm/services.pre.json  

Usage
-------------------
You can manage all OpenStack services the same way you would normally use the "service" command:  
**Start OpenStack Services**  

    [root@server ~]# service osm start  
    
**Stop OpenStack Services**  

    [root@server ~]# service osm stop  
    
**Print Service Status**  

    [root@server ~]# service osm status  
    
The above command will print a list of all pre-start services, and pre-start/stop commands.