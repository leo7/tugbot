### Create a dev environment for testing tugbot on Swarm cluster

```cli
# create a swarm manager virtual machine
$ docker-machine create --driver virtualbox manager1

# find ip/details on manager1 (created machine)
$ docker-machine env manager1
$ docker-machine ip manager1

# list of machines
docker-machine ls

# connect to manager1 client (like ssh)
$ eval $(docker-machine env manager1)

# initialize manager1 as swarm manager
$ docker swarm init --advertise-addr 192.168.99.100
Swarm initialized: current node (ceks8bcwkp2z4smewkx0i2z8h) is now a manager.

To add a worker to this swarm, run the following command:
    docker swarm join \
    --token SWMTKN-1-0ot43sramufgw93jijoh54q4o7ghe10zgaq7ljvqus1cv24gie-bbrziyhnvbq6f7yq31j6oowa6 \
    192.168.99.100:2377

To add a manager to this swarm, run the following command:
    docker swarm join \
    --token SWMTKN-1-0ot43sramufgw93jijoh54q4o7ghe10zgaq7ljvqus1cv24gie-6i30qe437o6n81v55oupvcyyr \

# create 2 nodes in cluster
$ docker-machine create --driver virtualbox worker1
$ docker-machine create --driver virtualbox worker2

# connect nodes to swarm cluster
$ eval $(docker-machine env <worker>)
$ docker swarm join \
      --token SWMTKN-1-0ot43sramufgw93jijoh54q4o7ghe10zgaq7ljvqus1cv24gie-bbrziyhnvbq6f7yq31j6oowa6 \
      192.168.99.100:2377
```