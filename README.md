VPLS - OpenStack Service Manager
===================

This is a set of scripts and JSON files to manage starting and stopping OpenStack and supporting services and commands. I"ve run into a lot of problem with server shutdowns and restarts, where OpenStack services don"t start up in the correct order causing a break in OpenStack functionality.  

Please note that this package has only been testing on RHEL/CentOS 6.x. You are welcome to try modifying it to support earlier revisions of RHEL/CentOS or other Linux platforms and submit the changes back here.  

Installation
-------------------

Copy the following files to the specified destinations on your CentOS 6.x server:  
* bin/osm -> /usr/bin/osm
* init.d/osm -> /etc/init.d/osm
* json/* -> /etc/osm/.  

Make sure both "osm" files are executable.  

Configuration
-------------------

To set the startup and shutdown order for OpenStack services, edit the "/etc/osm/services.json" file. To define which services should start and stop automatically at boot and shutdown, edit the "/etc/osm/services.run.json" file. To edit which services should start and stop prior to OpenStack services, as well as commands to run prior to startup/shutdown, edit the "/etc/osm/services.pre.json" file.