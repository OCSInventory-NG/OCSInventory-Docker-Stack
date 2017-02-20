<p align="center">
  <img src="https://cdn.ocsinventory-ng.org/common/banners/banner660px.png" height=200 width=508 alt="Banner">
</p>

<h1 align="center">OCS Inventory</h1>
<p align="center">
  <b>Some Links:</b><br>
  <a href="http://ask.ocsinventory-ng.org">Ask question</a> |
  <a href="#COMMING_SOON_STAY_CONNECTED">Installation</a> |
  <a href="http://www.ocsinventory-ng.org/?utm_source=github-ocs">Website</a> |
  <a href="https://www.factorfx.com/ocs-en">Support</a>
</p>

<p align='justify'>
OCS (Open Computers and Software Inventory Next Generation) is an assets management and deployment solution.
Since 2001, OCS Inventory NG has been looking for making software and hardware more powerful.
OCS Inventory NG asks its agents to know the software and hardware composition of every computer or server.
</p>




<h2 align="center">Assets management</h2>
<p align='justify'>
Since 2001, OCS Inventory NG has been looking for making software and hardware more powerful. OCS Inventory NG asks its agents to know the software and hardware composition of every computer or server. OCS Inventory also ask to discover network’s elements which can’t receive an agent. Since the version 2.0, OCS Inventory NG take in charge the SNMP scans functionality.
This functionality’s main goal is to complete the data retrieved from the IP Discover scan. These SNMP scans will allow you to add a lot more informations from your network devices : printers, scanner, routers, computer without agents, …
</p>

<h2 align="center">Deployment</h2>
<p align='justify'>
OCS Inventory NG includes the packet deployment functionality to be sure that all of the softwares environments which are on the network are the same. From the central management server, you can send the packets which will be downloaded with HTTP/HTTPS and launched by the agent on client’s computer. The OCS deployment is configured to make the packets less impactable on the network. OCS is used as a deployment tool on IT stock of more 100 000 devices.
</p>
<br />

###Docker Stack OCSInventory

This repository contains the needed files to build and run the OCS stack in his last version.
This stack is based on the official [Debian image](https://hub.docker.com/_/debian/) and official [MYSQL image](https://hub.docker.com/_/mysql/), you can find them on the [Docker hub](https://hub.docker.com/explore/).
We include a MYSQL container with pre-configured with the required database settings.

###Build instructions

We use docker-compose to build these images. Clone this repo and then:

> sudo git clone https://github.com/OCSInventory-NG/OCSInventory-Docker-Stack.git <br>
> cd OCSInventory-Docker-Stack <br>
> sudo docker-compose build 

This command will build all the images and pull the latest version.

----------
You can also find a prebuilt image for OCSInventory without MYSQL server from our [Docker Hub repository](https://hub.docker.com/r/ocsinventory/ocsinventory-docker-image/) or our [Github](https://github.com/OCSInventory-NG/OCSInventory-Docker-Image), which can be pulled with this command:

> sudo docker pull ocsinventory/ocsinventory-docker-image:master

###How to run it

By default, when the OCSInventory container is running it will load a default OCSInventory installation that is ready to be used. However, you can run the installer by defining one of these env variables, you can find them in the docker-compose.YML

####MYSQL container :

environment:

> MYSQL_ROOT_PASSWORD : changeme  <br>
> MYSQL_USER : ocs <br> 
> MYSQL_PASSWORD : ocs <br> 
> MYSQL_DATABASE : ocsweb 

----------

####OCSInventory-server container :

environment :

> OCS_DBNAME : ocsweb <br>
> OCS_DBSERVER_READ : ocsinventory-db <br>
> OCS_DBSERVER_WRITE : ocsinventory-db <br>
> OCS_DBUSER : ocs <br>
> OCS_DBPASS : ocs

These values are the default values for OCSInventory, if you want to change, you must change the configuration in z-ocsinventory-server.conf
After adjusting the docker-compose.yml, you can test the containers with docker-compose

> cd OCSInventory-Docker-Stack <br>
> sudo docker-compose build <br>
> sudo docker-compose up

This will bring up all needed containers, link them and mount data volumes according to the docker-compose.yml configuration file.

###Container shell access and viewing container logs

The docker exec command allows you to run commands inside a Docker container. The following command line will give you a bash shell inside your OCSInventory container:

> sudo docker exec -it ocsinventory-server bash

or

> sudo docker exec -it ocsinventory-db bash

You can access the logs from the container OCSInventory through Docker container log:

> sudo docker logs ocsinventory-server

or

> sudo docker logs ocsinventory-db

###Data Volume

Two volumes are created at the start of the stack OCSInventory. They contain the necessary information to ensure a proper functioning of OCS Inventory as well as MYSQL

By default:

**ocsdata** for the MYSQL service
   - /var/lib/mysql/

**ocssrv** for service OCSInventory 
   - /usr/share/ocsinventory-reports/
   - /etc/ocsinventory-reports/
   - /var/lib/ocsinventory-reports/

Attention do not remove these volumes without having planned backup, otherwise you will lose your data.

## Contributing

1. Fork it!
2. Create your feature branch: git checkout -b my-new-feature
3. Add your changes: git add folder/file1.php
4. Commit your changes: git commit -m 'Add some feature'
5. Push to the branch: git push origin my-new-feature
6. Submit a pull request !

## License

OCS Inventory Docker Stack is GPLv3 licensed
