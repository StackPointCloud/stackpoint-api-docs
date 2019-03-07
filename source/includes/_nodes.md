# Nodes

Each cluster in the StackPointCloud system can have 3 or more nodes.

## Get All Nodes of a Cluster

```shell
curl -x GET "https://api.stackpoint.io/orgs/4/clusters/12/nodes"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
``` 

> The above command returns JSON structured like this:

```json
[
    {
        "pk": 81,
        "cluster": 12,
        "pool": null,
        "pool_name": "",
        "instance_id": "spca44o3iw-master-1",
        "role": "master",
        "group_name": "",
        "private_ip": "10.136.53.103",
        "public_ip": "67.205.148.185",
        "platform": "coreos",
        "image": "coreos-stable",
        "channel": "stable",
        "location": "nyc1",
        "provider_subnet_id": "",
        "provider_subnet_cidr": "",
        "size": "2gb",
        "state": "running",
        "is_failed": false,
        "created": "2017-12-06T02:22:21.768702Z",
        "updated": "2017-12-07T02:20:57.216553Z"
    },
    {
        "pk": 82,
        "cluster": 12,
        "pool": 45,
        "pool_name": "Default Worker Pool",
        "instance_id": "spca44o3iw-worker-1",
        "role": "worker",
        "group_name": "autoscaling-spca44o3iw-pool-1",
        "private_ip": "10.136.28.7",
        "public_ip": "198.211.114.110",
        "platform": "coreos",
        "image": "coreos-stable",
        "channel": "stable",
        "location": "nyc1",
        "provider_subnet_id": "",
        "provider_subnet_cidr": "",
        "size": "2gb",
        "state": "running",
        "is_failed": false,
        "created": "2017-12-06T02:22:21.769636Z",
        "updated": "2017-12-07T02:20:57.224818Z"
    },
    {
        "pk": 83,
        "cluster": 12,
        "pool": 45,
        "pool_name": "Default Worker Pool",
        "instance_id": "spca44o3iw-worker-2",
        "role": "worker",
        "group_name": "autoscaling-spca44o3iw-pool-1",
        "private_ip": "10.136.30.245",
        "public_ip": "162.243.168.98",
        "platform": "coreos",
        "image": "coreos-stable",
        "channel": "stable",
        "location": "nyc1",
        "provider_subnet_id": "",
        "provider_subnet_cidr": "",
        "size": "2gb",
        "state": "running",
        "is_failed": false,
        "created": "2017-12-06T02:22:21.770540Z",
        "updated": "2017-12-07T02:20:57.226463Z"
    }
]
```

This endpoint retrieves all transitioning or running nodes under a given cluster.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/nodes`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster

## Get a Specific Node

```shell
curl "https://api.stackpoint.io/orgs/4/clusters/12/nodes/81"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
{
    "pk": 8927,
    "cluster": 2742,
    "pool": null,
    "pool_name": "",
    "instance_id": "spca44o3iw-master-1",
    "role": "master",
    "group_name": "",
    "private_ip": "10.136.53.103",
    "public_ip": "67.205.148.185",
    "platform": "coreos",
    "image": "coreos-stable",
    "channel": "stable",
    "location": "nyc1",
    "provider_subnet_id": "",
    "provider_subnet_cidr": "",
    "size": "2gb",
    "state": "running",
    "is_failed": false,
    "created": "2017-12-06T02:22:21.768702Z",
    "updated": "2017-12-07T02:20:57.216553Z"
}
```

This endpoint retrieves all transitioning or running nodes under a given cluster.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/nodes/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster
ID | ID of the node

## Add Nodes to a Cluster

Adding master and worker nodes require separate requests.

### Request Data Attributes

Parameter | Type | Description
--------- | ---- | -----------
role | string | Type of node to add. Options: `master`, `worker`
size | string | Instance size for the nodes. Consult provider documentation for available instance sizes.
node_count | integer | Number of nodes to add
node_pool | integer | ID of the node pool to add the node to. Valid only when adding workers. If no value is specified, default node pool will be used
zone | string | The zone where the node should be added. Valid only for master nodes on AWS
provider_subnet_id | string | ID of Subnet where node should be added. Valid only for master nodes on AWS
provider_subnet_cidr | string | Subnet CIDR. Valid only for master nodes on AWS

<aside class="warning">Only 1 master node should be added at a time.</aside>

## Add a Master Node

```shell
curl --header "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5" \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --request POST \
     --data @add_master_node.json \
     https://api.stackpoint.io/orgs/1/clusters/12/add_node
```

> `add_master_node.json` should contain the following data:

```json
{
    "node_count": 1,
    "size": "2gb",
    "role": "master"
}
```

Add a master node to a DigitalOcean cluster.

`POST https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/add_node`

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster

## Add Worker Nodes

```shell
curl --header "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5" \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --request POST \
     --data @add_worker_nodes.json \
     https://api.stackpoint.io/orgs/1/clusters/12/add_node
```

> `add_worker_nodes.json` should contain the following data:

```json
{
    "node_count": 3,
    "size": "2gb"
}
```

Add a worker node to a DigitalOcean cluster.

`POST https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/add_node`

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster

## Check Node Delete Eligiblity

```shell
curl -X GET "https://api.stackpoint.io/orgs/4/clusters/12/nodes/81/can_delete"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> If the node can be deleted, a JSON response is returned:

```json
{
    "eligible": True
}
```

> If the node can not be deleted, a JSON response is returned with status code `400`:

```json
{
    "detail": "Initial master node is essential to the cluster and can't be removed."
}
```

This endpoint checks whether a specific node can be deleted.

`GET https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/nodes/can_delete`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster
ID | ID of the node


## Delete a Node

```shell
curl -X DELETE "https://api.stackpoint.io/orgs/4/clusters/12/nodes/81"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns an empty response with status code `204`

This endpoint deletes a specific node.

`DELETE https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/nodes/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster
ID | ID of the node
