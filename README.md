## Docker-in-Docker example project for resin.io

This project demonstrates how to run docker-in-docker on a fleet of resin.io devices, allowing one to use docker-compose to bring up a composition of containers. In this example, define two container services, a python webserver and a redis store. The Python web server service has its 5000 port mapped port 80 of the hostOS, so one can see the webserver on the deviceURL.

### Important Notes:

* The daemon.json for docker should always define the default `dns` and `iptables=false`, if you change this, there is a good change you can break the dns resolution on the hostOS and your device won't be able to connect to resin.io anymore and will stop receiving updates.
* The docker daemon inside the resin.io container will need to use the correct storage driver. For raspberry pi 3, this is AUFS, for other boards like the Nvidia TX2, it will use overlay2. You can see this is their respective `daemon.json` files.
* The docker daemon you start in the container, will use the `/data` data partition to store its images. On the initial deployment, the device will need to pull those images and build them. If you purge `/data` for this device, all the docker images will be removed.
* Installs `docker v1.13.1` and `docker-compose v1.8.0`

### Tested on:

* Raspberry Pi 3
    * Resin OS 2.7.5+rev1 (dev)
    * Resin OS 2.7.8+rev1 (dev)
* Intel Edison
    * Resin OS 2.7.8+rev1 (dev)