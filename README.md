This page shows you how to setup swarm hybrid cluster for virualbox and raspberry pi.

Prerequisites -
1) Docker machine
2) Virtualbox
3) Raspberry Pi

Step by step guide :
This will assume that you have a windows machine, for linux based systems the steps would be little different.
Install Docker machine and Virtualbox. Also make sure the Pi is configured properly. 

1) Create the swarm cluster 
docker run swarm create ---> token

2) Create the swarm master
docker-machine create -d virtualbox --swarm --swarm-master --swarm-discovery token://<token_id> swarm-master

3) Create swarm node 1 (virtualbox machine)
docker-machine create -d virtualbox --swarm --swarm-discovery token://<token_id> swarm-node-01

3) Create swarm node 2 (pi machine)
docker-machine create -d hypriot --swarm --swarm-discovery token://<token_id> swarm-node-02

