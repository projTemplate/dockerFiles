### get info about garace
> docker exec -ti ksa-garage /garage

### to check status

> docker exec -ti ksa-garage /garage status

### Creating a cluster layout
Creating a cluster layout for a Garage deployment means informing Garage of the disk space available on each node of the cluster as well as the zone (e.g. datacenter) each machine is located in.

For our test deployment, we are using only one node. The way in which we configure it does not matter, you can simply write:

> garage layout assign -z dc1 -c 1G <node_id>
docker exec -ti ksa-garage /garage layout assign -z dc1 -c 1 f193e45e2b11ccfc

where <node_id> corresponds to the identifier of the node shown by garage status (first colum

### The layout then has to be applied to the cluster, using:

docker exec -ti ksa-garage /garage layout show
### garage layout apply
docker exec -ti ksa-garage /garage layout apply --version 1

### create a bucket
docker exec -ti ksa-garage /garage bucket create delta


## Create an api key

docker exec -ti ksa-garage /garage key new --name delta-app-key

## allow this key to read and write on bucket delta
docker exec -ti ksa-garage /garage bucket allow --read --write --owner delta --key delta-app-key 

## allow web access for delta bucket
docker exec -ti ksa-garage /garage bucket website delta --allow 