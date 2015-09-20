This page shows you how to setup swarm hybrid cluster for virtualbox and raspberry pi.

Prerequisites -
1) Docker machine
2) Virtualbox
3) Raspberry Pi

Step by step guide :
This will assume that you have a windows machine, for linux based systems the steps would be little different.
Install Docker machine and Virtualbox. Also make sure the Pi is configured properly. 

1) Create the swarm cluster 
docker run swarm create ---> $TOKEN

2) Create the swarm master 
docker-machine create -d hypriot --swarm --swarm-master --swarm-discovery token://$TOKEN --hypriot-ip-address 192.168.1.100 pi1

3) Create swarm node 2 (virtualbox machine)
docker-machine create -d virtualbox --swarm --swarm-discovery token://$TOKEN vb1

To check if everything works we can connect to the newly started Swarm Master by using the following command. It retrieves all environment variables needed for the Docker client to communicate with the Swarm.

$ eval $(./docker-machine env --swarm pi1)
$ docker info
Containers: 2
Strategy: spread
Filters: affinity, health, constraint, port, dependency
Nodes: 1
 pi1: 192.168.1.100:2375
  └ Containers: 2
  └ Reserved CPUs: 0 / 4
  └ Reserved Memory: 0 B / 971.3 MiB

Additional containers for Python and MySQL are also created on the Raspberry PI

$ docker ps
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS              PORTS                              NAMES
07dcce706293        hypriot/rpi-swarm:latest   "/swarm join --advert"   46 minutes ago      Up 21 minutes       2375/tcp                           swarm-agent
121fd19fbce4        hypriot/rpi-swarm:latest   "/swarm manage --tlsv"   46 minutes ago      Up 21 minutes       2375/tcp, 0.0.0.0:3376->3376/tcp   swarm-agent-master
bebaa859f8b7        hypriot/rpi-python         "/bin/bash"              About an hour ago   Up 21 minutes       0.0.0.0:80->80/tcp                 Python4
8400ad611230        hypriot/rpi-mysql          "/entrypoint.sh /bin/"   3 hours ago         Up 21 minutes       3306/tcp                           MYSQL

PS: There are some issues when docker tries to retreive information from the swarm master as the SSH command
intermittently returns an error and displays stale information.



