# swarmpi

Managing the raspberry pi and virtualbox machines with Hybrid Swam

Steps to follow -

1) Create the swarm cluster 
docker run swarm create ---> token

2) Create the swarm master
docker-machine create -d virtualbox --swarm --swarm-master --swarm-discovery token://<token_id> swarm-master

3) Create swarm nodes
docker-machine create -d virtualbox --swarm --swarm-discovery token://<token_id> swarm-node-01

3) Create swarm nodes
docker-machine create -d hypriot --swarm --swarm-discovery token://<token_id> swarm-node-01

