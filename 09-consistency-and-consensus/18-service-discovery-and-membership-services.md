# Service Discovery and Membership Services

- Zookeeper etcd and Consul are also often used for service discovery, that is to find which IP address need to connect in order to reach a particular service.

- In cloud data center envs it is common for virtual machines to come and go continually , we dont know the IP address of the service ahead of time , Instead we can configure service to register when they startup they register their network endpoints in a service registry, where they can be founded by other services.


---

# Membership Services

- A membership service determines which nodes are currently active and live members of a cluster. 
