Image for running Oracle Database 11g Standard/Enterprise. Due to oracle license restrictions image is not contain database itself and will install it on first run from external directory.

``This image for development use only``

# Usage
Download database installation files from [Oracle site](http://www.oracle.com/technetwork/database/in-memory/downloads/index.html) and unpack them to **install_folder**.
Run container and it will install oracle and create database:

```sh
docker run --privileged --name oracle11g -p 1521:1521 -v <install_folder>:/install jaspeen/oracle-11g
```
Then you can commit this container to have installed and configured oracle database:
```sh
docker commit oracle11g oracle11g-installed
```

Database located in **/opt/oracle** folder

OS users:
* root/install
* oracle/install

DB users:
* SYS/oracle

Optionally you can map dpdump folder to easy upload dumps:
```sh
docker run --privileged --name oracle11g -p 1521:1521 -v <install_folder>:/install -v <local_dpdump>:/opt/oracle/dpdump jaspeen/oracle-11g
```
Example:
```sh
docker run --privileged --name oracle11g -p 1521:1521 -v /home/elessar/Documents/oracle11g:/install -v /home/elessar/Documents/oracle11g/dpdumps:/opt/oracle/dpdumps jaspeen/oracle-11g
```
The directory /home/elessar/Documents/oracle11g contains the unzip folder "database" and the directory /home/elessar/Documents/oracle11g/dpdumps is the local directory for mapping to dumps directory in oracle container.

To execute impdp/expdp just use docker exec command:
```sh
docker exec -it oracle11g impdp ..
```
To execute bash:
```sh
docker exec -it oracle11g bash
```
or:
```sh
docker exec -it oracle11g /bin/bash
```
