# NodePools

Node pools are used to manage worker nodes with common properties.

Each cluster gets a default node pool when it is created. Master nodes are stand-alone and do not belong to pools.

## Get All Nodepools of a Cluster

```shell
curl "https://api.stackpoint.io/orgs/4/clusters/12/nodepools"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
[
    {
        "pk": 37,
        "cluster": 12,
        "name": "Default Worker Pool",
        "instance_id": "spca44o3iw-pool-1",
        "instance_size": "2gb",
        "platform": "coreos",
        "channel": "stable",
        "zone": "nyc1",
        "provider_subnet_id": "",
        "provider_subnet_cidr": "",
        "node_count": 2,
        "role": "worker",
        "state": "active",
        "is_default": true,
        "created": "2017-12-06T02:22:21.767822Z",
        "updated": "2017-12-06T02:22:21.797813Z"
    },
    {
        "pk": 38,
        "cluster": 12,
        "name": "High Memory Pool",
        "instance_id": "spca44o3iw-pool-1",
        "instance_size": "4gb",
        "platform": "coreos",
        "channel": "stable",
        "zone": "nyc1",
        "provider_subnet_id": "",
        "provider_subnet_cidr": "",
        "node_count": 4,
        "role": "worker",
        "state": "active",
        "is_default": false,
        "created": "2017-12-06T02:22:21.767822Z",
        "updated": "2017-12-06T02:22:21.797813Z"
    }
]
```

This endpoint retrieves all transitioning or running nodes under a given cluster.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/nodepools`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster

## Get a Specific Nodepool

```shell
curl "https://api.stackpoint.io/orgs/4/clusters/12/nodepools/37"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
{
    "pk": 37,
    "cluster": 12,
    "name": "Default Worker Pool",
    "instance_id": "spca44o3iw-pool-1",
    "instance_size": "2gb",
    "platform": "coreos",
    "channel": "stable",
    "zone": "nyc1",
    "provider_subnet_id": "",
    "provider_subnet_cidr": "",
    "node_count": 2,
    "role": "worker",
    "state": "active",
    "is_default": true,
    "created": "2017-12-06T02:22:21.767822Z",
    "updated": "2017-12-06T02:22:21.797813Z"
}
```

This endpoint retrieves all transitioning or running nodes under a given cluster.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/nodepools/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster
ID | ID of the node pool

## Create a Nodepool

### Request Data Attributes

Parameter | Type | Description
--------- | ---- | -----------
name | string | Name of the nodepool
instance_size | string | Instance size for the nodes. Consult provider documentation for available instance sizes.
node_count | integer | Number of nodes to add
platform | string | Linux distribution to use. Options are:
 | | AWS: `coreos`, `ubuntu`
 | | Azure: `coreos`, `ubuntu`
 | | DigitalOcean: `coreos`, `ubuntu`
 | | GCE: `coreos`, `ubuntu`
 | | GKE: `gci` (send gci for "cos" as well)
zone | string | The zone where the node should be added. Valid only for master nodes on AWS
provider_subnet_id | string | ID of Subnet where node should be added. Valid only for master nodes on AWS
provider_subnet_cidr | string | Subnet CIDR. Valid only for master nodes on AWS

## Create a GCE Nodepool

```shell
curl --header "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5" \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --request POST \
     --data @add_node_pool.json \
     https://api.stackpoint.io/orgs/1/clusters/12/nodepools
```

> `add_node_pool.json` should contain the following data:

```json
{
    "name": "Awesome Node Pool",
    "instance_size": "n1-standard-2",
    "node_count": 4,
    "platform": "coreos"
}
```

This endpoint allows creating a new Nodepool resource.

### HTTP Request

`POST https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<CLUSTER_ID>/nodepools`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
CLUSTER_ID | ID of the cluster
