# Nodes

Each cluster in the StackPointCloud system can have 3 or more nodes.

## GET All Nodes

```shell
GET https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}/nodes
```

> Example query:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/clusters/2/nodes"
```

> Example response:

```json
[
  {
    "pk": 6,
    "cluster": 2,
    "pool": 2,
    "pool_name": "Default Worker Pool",
    "instance_id": "spc8brwf3x-worker-2",
    "provider_node_id": "",
    "role": "worker",
    "group_name": "autoscaling-spc8brwf3x-pool-1",
    "private_ip": "",
    "public_ip": "",
    "platform": "coreos",
    "image": "ami-0b0f4f5f0c8c1a797",
    "channel": "stable",
    "etcd_state": "none",
    "root_disk_size": 50,
    "gpu_instance_size": "",
    "gpu_core_count": null,
    "location": "us-west-2:us-west-2a",
    "zone": "us-west-2a",
    "provider_subnet_id": "subnet-d19044b6",
    "provider_subnet_cidr": "172.22.4.0\/24",
    "size": "t2.large",
    "state": "draft",
    "is_failed": false,
    "created": "2019-02-15T16:28:01.495851Z",
    "updated": "2019-02-15T16:28:01.496121Z"
  }
]
```
Get details for all of the transitioning or running nodes for the specified cluster.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Node ID.
**cluster** | Cluster ID.
**pool** | Node pool ID
**pool_name** | Node pool name.
**instance_id** | Instance ID.
**provider_node_id** | Provider node ID.
**role** | The node's role. Allowed values are `master` and `worker`.
**group_name** | Group name.
**private_ip** | The node's private IP address.
**public_ip** | The node's public IP address.
**platform** | The node's operating system.
**image** | The image used.
**channel** | The cluster's OS distribution version.
**etcd_state** | The state of etcd (if applicable).
**root_disk_size** | Root disk size.
**gpu_instance_size** | GPU instance size.
**gpu_core_count** | GPU core count.
**location** | Location.
**zone** | The AWS provider zone. Valid only for master nodes on AWS.
**provider_subnet_id** | ID of the subnet where the node has been added. Valid only for master nodes on AWS.
**provider_subnet_cidr** | The subnet CIDR. Valid only for master nodes on AWS.
**size** | Node size.
**state** | The node's state.
**is_failed** | Whether or not the node has failed.

## GET a Specific Node

```shell
GET https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}/nodes/{Node ID}
```

> Example query:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/clusters/2/nodes/6"
```

> Example response:

```json
[
  {
    "pk": 6,
    "cluster": 2,
    "pool": 2,
    "pool_name": "Default Worker Pool",
    "instance_id": "spc8brwf3x-worker-2",
    "provider_node_id": "",
    "role": "worker",
    "group_name": "autoscaling-spc8brwf3x-pool-1",
    "private_ip": "",
    "public_ip": "",
    "platform": "coreos",
    "image": "ami-0b0f4f5f0c8c1a797",
    "channel": "stable",
    "etcd_state": "none",
    "root_disk_size": 50,
    "gpu_instance_size": "",
    "gpu_core_count": null,
    "location": "us-west-2:us-west-2a",
    "zone": "us-west-2a",
    "provider_subnet_id": "subnet-d19044b6",
    "provider_subnet_cidr": "172.22.4.0\/24",
    "size": "t2.large",
    "state": "draft",
    "is_failed": false,
    "created": "2019-02-15T16:28:01.495851Z",
    "updated": "2019-02-15T16:28:01.496121Z"
  }
]
```
Get details for all of the transitioning or running nodes for the specified cluster.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.
**Node ID** | Yes | The Node ID.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Node ID.
**cluster** | Cluster ID.
**pool** | Node pool ID
**pool_name** | Node pool name.
**instance_id** | Instance ID.
**provider_node_id** | Provider node ID.
**role** | The node's role. Allowed values are `master` and `worker`.
**group_name** | Group name.
**private_ip** | The node's private IP address.
**public_ip** | The node's public IP address.
**platform** | The node's operating system.
**image** | The image used.
**channel** | The cluster's OS distribution version.
**etcd_state** | The state of etcd (if applicable).
**root_disk_size** | Root disk size.
**gpu_instance_size** | GPU instance size.
**gpu_core_count** | GPU core count.
**location** | Location.
**zone** | The AWS provider zone. Valid only for master nodes on AWS.
**provider_subnet_id** | ID of the subnet where the node has been added. Valid only for master nodes on AWS.
**provider_subnet_cidr** | The subnet CIDR. Valid only for master nodes on AWS.
**size** | Node size.
**state** | The node's state.
**is_failed** | Whether or not the node has failed.

## POST Add Nodes to a Cluster

```shell
POST "https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}/add_node"
```

Add nodes to the specified cluster.

<aside class="notice">Adding master and worker nodes requires separate requests.</aside>

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.

### Node Attributes

**Name** | **Type** | **Description**
---------|----------|----------------
**role** | string | Type of node to add. Allowed values are `master` or `worker`.
**size** | string | Instance size for the nodes. Consult provider documentation for available instance sizes.
**node_count** | integer | Number of nodes to add.
**node_pool** | integer | ID of the node pool to add the node to. Valid only when adding worker nodes. If no value is specified, the default node pool will be used.
**zone** | the zone where the node should be added. Valid only for master nodes on AWS.
**provider_subnet_id** | ID of the subnet where the node has been added. Valid only for master nodes on AWS.
**provider_subnet_cidr** | The subnet CIDR. Valid only for master nodes on AWS.

<aside class="warning">Only one master node should be added at a time.</aside>

## Example: Add a Master Node

```shell
POST "https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}/add_node"
```
> Example request:

```shell
curl -X POST \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-d @add-master-node.json \
https://api.stackpoint.io/orgs/1/clusters/2/add_node
```

> Contents of add-master-node.json:

```json
{
    "node_count": 1,
    "size": "2gb",
    "role": "master"
}
```

## GET a Node's Delete Eligibility

```shell
GET https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}/nodes/{Node ID}/can_delete
```

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/clusters/2/nodes/4/can_delete"
```

> Example response, if the node can be deleted:

```json
{
    "eligible": True
}
```

> If the node cannot be deleted, a JSON response is returned with status code `400`:

```json
{
    "detail": "Initial master node is essential to the cluster and can't be removed."
}
```
Get information on whether or not a specific node can be deleted.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.
**Node ID** | Yes | The Node ID.


## Delete a Node

```shell
DELETE "https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}/nodes/{Node ID}"
```
> Example request:

```shell
curl -X DELETE \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/clusters/2/nodes/4"
```

> If the node is successfully deleted, this command returns an empty response with status code `204`

Delete a specific node.

<aside class="warning">Before attempting to delete a node, check the `can_delete` endpoint (described above) to see if it can be deleted.</aside>

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.
**Node ID** | Yes | The Node ID.
