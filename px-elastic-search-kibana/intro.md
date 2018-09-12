[Portworx](https://portworx.com/) is a software defined persistent storage solution designed and purpose built for applications deployed as containers, via container orchestrators such as Kubernetes, Marathon and Swarm. It is a clustered block storage solution and provides a Cloud-Native layer from which containerized stateful applications programmatically consume block, file and object storage services directly through the scheduler.

This tutorial will provide you with a step by step guide in deploying the Elasticstack (Elastic Search, Logstash, Kibana) with Portworx on Kubernetes.

### High Level Overview

Elasticsearch creates a cluster based on the cluster name property specified in the configuration. Each node within the cluster can forward client requests to the appropriate node and also knows about every other node in the cluster.

An Elasticsearch cluster node can have one or more purposes.

Master-eligible node A node that has node.master set to true (default), which makes it eligible to be elected as the master node, which controls the cluster.

Data node A node that has node.data set to true (default). Data nodes hold data and perform data related operations such as CRUD, search, and aggregations.

Client node A node which only routes requests, handles the search reduce phase, and distributes bulk indexing. Consumers of the elastic search cluster interact with the client nodes.


### Other things you should know

To learn more about how why running PostgreSQL on Portworx is a great idea take a look at the following links:
* [Introduction to Portworx](https://portworx.com/products/introduction/)
* [Customer Stories](https://portworx.com/customers/)
* [STORK open source project](https://portworx.com/stork-storage-orchestration-kubernetes/).


This scenario assumes you have already covered the following scenarios:
* [How to install Portworx on Kubernetes](https://www.katacoda.com/portworx/scenarios/deploy-px-k8s)
* [How to create Portworx volumes on Kubernetes](https://www.katacoda.com/portworx/scenarios/px-k8s-vol-basic)
