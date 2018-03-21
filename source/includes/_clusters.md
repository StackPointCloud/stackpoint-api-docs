# Clusters

Clusters are one of the most important resource in the StackPointCloud system.

Clusters are scoped under organizations as well as workspaces.

<aside class="info">You need to find your [organization ID(s)](#get-all-organizations) and [keyset IDs](#get-all-keysets) in order to work with cluster endpoints.</aside>

## Get All Clusters

The `pk` attribute in the response denotes the cluster ID.

```shell
curl "https://api.stackpoint.io/orgs/4/clusters"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
[
    {
        "pk": 45,
        "instance_id": "spcbsk7u4u",
        "name": "SPC Wild Mouse",
        "org": 4,
        "provider": "do",
        "workspace": {
            "pk": 4,
            "name": "Default",
            "slug": "default",
            "org": 4,
            "is_default": true,
            "created": "2016-12-03T04:42:29.612800Z"
        },
        "k8s_version": "v1.8.3",
        "node_count": 3,
        "etcd_type": "self_hosted",
        "platform": "coreos",
        "channel": "stable",
        "region": "nyc1",
        "zone": "",
        "state": "draft",
        "solutions": [
            {
                "pk": 4409,
                "name": "Helm Tiller",
                "solution": "helm_tiller",
                "state": "draft"
            }
        ],
        "is_failed": false,
        "federation_role": null,
        "version_migrations": [],
        "k8s_rbac_enabled": true
    },
    {
        "pk": 46,
        "instance_id": "spcev1uzsp",
        "name": "SPC Late Mouse",
        "org": 4,
        "provider": "aws",
        "workspace": {
            "pk": 4,
            "name": "Default",
            "slug": "default",
            "org": 4,
            "is_default": true,
            "created": "2016-12-03T04:42:29.612800Z"
        },
        "k8s_version": "v1.8.3",
        "node_count": 3,
        "etcd_type": "self_hosted",
        "platform": "coreos",
        "channel": "stable",
        "region": "us-west-2",
        "zone": "us-west-2a",
        "state": "draft",
        "solutions": [
            {
                "pk": 4406,
                "name": "Helm Tiller",
                "solution": "helm_tiller",
                "state": "draft"
            },
            {
                "pk": 4407,
                "name": "Cloudflare Warp Ingress",
                "solution": "cloudflare-warp-ingress",
                "state": "draft"
            },
            {
                "pk": 4408,
                "name": "Prometheus",
                "solution": "prometheus",
                "state": "draft"
            }
        ],
        "is_failed": false,
        "federation_role": null,
        "version_migrations": [],
        "k8s_rbac_enabled": true
    }
]
```

This endpoint retrieves all clusters available under a specific organization.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ORG_ID>/clusters`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization


## Get a Specific Cluster

```shell
curl "https://api.stackpoint.io/orgs/4/clusters/45"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
{
    "pk": 45,
    "name": "SPC Wild Mouse",
    "org": 4,
    "site": 6,
    "workspace": {
        "pk": 4,
        "name": "Default",
        "slug": "default",
        "org": 4,
        "is_default": true,
        "created": "2016-12-03T04:42:29.612800Z"
    },
    "instance_id": "spcbsk7u4u",
    "provider": "do",
    "provider_keyset": 78,
    "provider_keyset_name": "My DO Keyset",
    "region": "nyc1",
    "platform": "coreos",
    "channel": "stable",
    "state": "draft",
    "project_id": "",
    "owner": 3,
    "user_ssh_keyset": 66,
    "user_ssh_keyset_name": "Default SPC SSH Keypair",
    "etcd_type": "self_hosted",
    "provider_network_id": null,
    "provider_network_cidr": null,
    "provider_subnet_id": null,
    "provider_subnet_cidr": null,
    "provider_balancer_id": null,
    "config": {},
    "layout": {},
    "solutions": [
        {
            "pk": 4409,
            "name": "Helm Tiller",
            "instance_id": "sol635cuqs",
            "cluster": 2745,
            "solution": "helm_tiller",
            "installer": "ansible_custom",
            "keyset": null,
            "keyset_name": "",
            "state": "draft",
            "url": "",
            "username": "",
            "password": "",
            "max_nodes": null,
            "git_repo": "",
            "git_path": "",
            "config": {},
            "extra_data": {},
            "created": "2017-12-06T19:37:13.002023Z",
            "updated": "2017-12-06T19:37:13.002045Z",
            "is_deleteable": false
        }
    ],
    "features": [],
    "notified": false,
    "created": "2017-12-06T19:37:11.896350Z",
    "updated": "2017-12-06T19:37:12.993133Z",
    "k8s_version": "v1.8.3",
    "k8s_dashboard_enabled": true,
    "k8s_rbac_enabled": true,
    "k8s_etcd_operator_installed": false,
    "k8s_dashboard_installed": false,
    "k8s_pod_cidr": "10.2.0.0/16",
    "k8s_service_cidr": "10.3.0.0/24",
    "is_kubeconfig_available": false,
    "kubeconfig_path": "/orgs/4/clusters/2745/kubeconfig",
    "node_count": 3,
    "master_count": 1,
    "master_size": "2gb",
    "image": "coreos-stable",
    "zone": "",
    "is_k8s_available": false,
    "is_failed": false,
    "federation_role": null,
    "k8s_etcd_cluster": null,
    "is_etcd_host": false,
    "version_migrations": []
}
```

This endpoint retrieves a specific cluster available under a specific organization.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
ID | ID of the cluster

## Create a Cluster

The cluster creation request varies slightly from one provider to the other.

### Request Data Attributes

#### Cluster Attributes

Parameter | Type | Description
--------- | ---- | -----------
name | string | Name of the cluster, must be unique within an organization
provider | string | Any of: AWS: `aws`, Azure: `azure`, DigitalOcean: `do`, GCE: `gce`, GKE: `gke`
provider_keyset | integer | ID of the provider keyset
master_count | integer | Number of master. Only valid value for cluster creation request is `1`
master_size | string | Size of master. Consult provider documentation for instance sizes
worker_count | integer | Number of workers. Minimum value `2`
worker_size | string | A single size for all workers. Consult provider documentation for instance sizes
region | string | Provider region value. For GCE and GKE, send Google's "Zone" value here
zone | string | Provider zone. AWS only
provider_network_id | string | VPC ID. AWS only
provider_network_cidr | string | VPC CIDR. AWS only
provider_subnet_id | string | Subnet ID. AWS only
provider_subnet_cidr | string | Subnet CIDR. AWS only
k8s_version | string | Version of Kubernetes. Current options are: `v1.7.10`, `'v1.8.3`
k8s_rbac_enabled | boolean | Specify if you want RBAC enabled
k8s_dashboard_enabled | boolean | Specify if you want dhasboard installed
etcd_type | string | Where to host etcd. Only valid value is `self_hosted`
platform | string | Linux distribution to use. Options are:
 | | AWS: `coreos`, `ubuntu`
 | | Azure: `coreos`, `ubuntu`
 | | DigitalOcean: `coreos`, `ubuntu`
 | | GCE: `coreos`, `ubuntu`
 | | GKE: `gci`
channel | string | Distribution version to use. Options are:
 | | CoreOS: `stable`, `beta`, `alpha`
 | | Ubuntu: `16.04-lts`
 | | GCI: `stable`
user_ssh_keyset | integer | ID of the SSH keyset that contains the public key to be used to SSH into nodes
solutions | A list of solution objects

#### Solution Attributes

Parameter | Type | Description
--------- | ---- | -----------
solution | string | Solution to be installed. Current options are: `istio`, `fabric8`, `turbonomic`, `cloudflare-warp-ingress`, `prometheus`, `efk`, `sysdig`, `haproxy`, `linkerd`, `netsil`, `autoscaler`, `helm_tiller`, `gitlab`, `gitlab_ee`, `kubeless`, `calico`
keyset | integer | ID of the solution keyset to use. Must belong to same organization (and workspace if applicable) as the cluster. Valid only for solutions: `turbonomic` and `sysdig`
max_nodes | integer | Number of nodes the autoscaler should scale to. Valid only for `autoscaler`

### HTTP Request

To create cluster in the default workspace use:

`POST https://api.stackpoint.io/orgs/<ORG_ID>/clusters`

To create a cluster under a specific workspace use:

`POST https://api.stackpoint.io/orgs/<ORG_ID>/workspaces/<WORKSPACE_ID>/clusters`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
WORKSPACE_ID | ID of a workspace under the organization

## Create an AWS Cluster

```shell
curl --header "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5" \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --request POST \
     --data @create_aws_cluster.json \
     https://api.stackpoint.io/orgs/1/clusters
```

> `create_aws_cluster.json` should contain the following data:

```json
{
    "name": "SPC Late Mouse",
    "provider": "aws",
    "provider_keyset": 55,
    "master_count": 1,
    "master_size": "t2.large",
    "worker_count": 2,
    "worker_size": "t2.large",
    "region": "us-west-2",
    "zone": "us-west-2a",
    "provider_network_id": "vpc-c4a6f5a0"
    "provider_network_cidr": "172.22.0.0/16",
    "provider_subnet_id": "subnet-d19044b6",
    "provider_subnet_cidr": "172.22.4.0/24",
    "k8s_version": "v1.8.3",
    "k8s_rbac_enabled": true,
    "k8s_dashboard_enabled": true,
    "etcd_type": "self_hosted",
    "platform": "coreos",
    "channel": "stable",
    "user_ssh_keyset": 66,
    "solutions": [
        {
            "solution": "helm_tiller",
        },
        {
            "solution": "cloudflare-warp-ingress",
        },
        {
            "solution": "prometheus",
        }
    ]
}
```

Create an AWS cluster and install Helm, Cloudflare Warp Ingress and Prometheus.

## Create a DigitalOcean Cluster

```shell
curl --header "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5" \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --request POST \
     --data @create_do_cluster.json \
     https://api.stackpoint.io/orgs/1/clusters
```

> `create_do_cluster.json` should contain the following data:

```json
{
    "name": "SPC Wild Night",
    "provider": "do",
    "provider_keyset": 56,
    "master_count": 1,
    "master_size": "2gb",
    "worker_count": 2,
    "worker_size": "2gb",
    "region": "nyc1",
    "k8s_version": "v1.8.3",
    "k8s_rbac_enabled": true,
    "k8s_dashboard_enabled": true,
    "etcd_type": "self_hosted",
    "platform": "coreos",
    "channel": "stable",
    "user_ssh_keyset": 66
}
```

Create a DigitalOcean cluster.

## Delete a Cluster

```shell
curl -X DELETE "https://api.stackpoint.io/orgs/1/clusters/25"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns an empty response with status code `204`

This endpoint will delete the cluster and all nodes, solutions and volumes associated with it.

`DELETE https://api.stackpoint.io/orgs/<ORG_ID>/clusters/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
ID | ID of the cluster
