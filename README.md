# k8sTheHardWay
#### Following along with Kelsey Hightower's 'Kubernetes the Hard Way' course.

After installing dependencies...


### Provisioning Compute Resources:
* Networking
  * Note: The Kubernetes networking model assumes a flat network in which containers and nodes can communicate with each other. In cases where this is not desired network policies can limit how groups of containers are allowed to communicate with each other and external network endpoints. Setting up network policies is out of scope for this tutorial.
    * The network policy capability would be useful in the case of a cluster with multiple applications and environments running inside it. In these cases, it can be more secure and organized if network policies are setup.

1. Create a VPC to host the cluster, named `kubernetes-the-hard-way`.
```
gcloud compute networks create kubernetes-the-hard-way --subnet-mode customer
```
2. Provision a subnet (named `kubernetes`) with an IP range large enough to assign a private IP to each node in the cluster (and any additional services added later on). And remember, an IP with the `/32` range has 1 IP. every number smaller than that doubles.
```
gcloud compute networks subnets create kubernetes \
  --network kubernetes-the-hard-way \
  --range 10.240.0.0/24
```
