# Clusters

The Clusters resource lets you create, manage, and delete Kubernetes clusters on the NKS system.

Clusters are scoped under Organizations as well as Workspaces.


## GET All Clusters

```shell
GET "https://api.stackpoint.io/orgs/{Org ID}/clusters"
```

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/2/clusters"
```

> Example response:

```json
[
    {
        "pk": 45,
        "instance_id": "spcbsk7u4u",
        "name": "My Cluster",
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
    }
]
```

Get all the Clusters belonging to the specified Organization.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | The Cluster ID.
**instance_id** | The cluster's instance name.
**name** | Cluster name.
**org** | Organization ID.
**provider** | The provider on which the cluster is provisioned.
**workspace** | The workspace (if applicable) to which the cluster is assigned.
**k8s_version** | The Kubernetes version.
**node_count** | Number of nodes.
**etcd_type** | The type of etcd server.
**platform** | The cluster's operating system.
**channel** | The cluster's OS distribution version.
**region** | The region in which the cluster is provisioned.
**zone** | The AWS provider zone. This value is blank for non-AWS clusters.
**state** | The cluster's current state.
**solutions** | Solutions (if any) which have been added to the cluster.
**is_failed** | This value is `true` if the cluster has failed, and `false` if the cluster is running.
**federation_role** | Whether or not the cluster has been Federated.
**k8s_rbac_enabled** | Whether or not the cluster has RBAC enabled.


## GET a Specific Cluster

```shell
GET "https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}"
```

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/2/clusters/45"
```

> Example response:

```json

    {
        "pk": 45,
        "instance_id": "spcbsk7u4u",
        "name": "My Cluster",
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
    }
```

Get information for a specific cluster.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | The Cluster ID.
**instance_id** | The cluster's instance name.
**name** | Cluster name.
**org** | Organization ID.
**provider** | The provider on which the cluster is provisioned.
**workspace** | The workspace (if applicable) to which the cluster is assigned.
**k8s_version** | The Kubernetes version.
**node_count** | Number of nodes.
**etcd_type** | The type of etcd server.
**platform** | The cluster's operating system.
**channel** | The cluster's OS distribution version.
**region** | The region in which the cluster is provisioned.
**zone** | The AWS provider zone. This value is blank for non-AWS clusters.
**state** | The cluster's current state.
**solutions** | Solutions (if any) which have been added to the cluster.
**is_failed** | This value is `true` if the cluster has failed, and `false` if the cluster is running.
**federation_role** | Whether or not the cluster has been Federated.
**k8s_rbac_enabled** | Whether or not the cluster has RBAC enabled.

## GET a Cluster's Kubeconfig File

```shell
GET "https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}/kubeconfig"
```

> Example request. The following request will pipe the results of the query into the local file `kubeconfig` which you can then use to work with your cluster.

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/2/clusters/14/kubeconfig" \
> kubeconfig
```

Download the kubeconfig file for the specified cluster.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.

## POST Create a Cluster

> To create a cluster in the default workspace:

```shell
POST "https://api.stackpoint.io/orgs/{Org ID}/clusters"
```

> To create a cluster in a specific workspace:

```shell
POST "https://api.stackpoint.io/orgs/{Org ID}/workspaces/{Workspace ID}/clusters"
```

Create a cluster in the specified Organization and (optional) Workspace.

<aside class="notice">The cluster creation request varies slightly between providers.</aside>

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.
**Workspace ID** | No | The Workspace ID.

### Cluster Attributes

**Name** | **Type** | **Description**
--------- | ---- | -----------
**name** | string | Name of the cluster, must be unique within an organization.
**provider** | string | Allowed values are `aks`, `aws`, `azure`, `eks`, `gce`, or `gke`.
**provider_keyset** | integer | ID of the provider keyset.
**master_count** | integer | Number of masters. The only valid value for a cluster creation request is `1`.
**master_size** | string | Size of the master. Consult provider documentation for allowed instance sizes.
**worker_count** | integer | Number of workers. The minimum value is `2`.
**worker_size** | string | A single size for all workers. Consult provider documentation for allowed instance sizes.
**region** | string | Provider region value. For GCE and GKE, use Google's "Zone" value.
**zone** | string | Provider zone. AWS only.
**provider_network_id** | string | VPC ID. AWS only.
**provider_network_cidr** | string | VPC CIDR. AWS only.
**provider_subnet_id** | string | Subnet ID. AWS only.
**provider_subnet_cidr** | string | Subnet CIDR. AWS only.
**k8s_version** | string | Version of Kubernetes. The current options are `v1.12.4` or `'v1.13.2.`.
**k8s_rbac_enabled** | boolean | Specify if you want to enable RBAC.
**k8s_dashboard_enabled** | boolean | Specify if you want to enable the dashboard.
**etcd_type** | string | Where to host etcd. Only valid value is `self_hosted`.
**platform** | string | Linux distribution to use. The allowed values are:
 | | AWS: `coreos`, `ubuntu`
 | | Azure: `coreos`, `ubuntu`
 | | GCE: `coreos`, `ubuntu`
 | | GKE: `gci` (send gci for "cos" as well)
channel | string | Distribution version to use. Options are:
 | | CoreOS: `stable`, `beta`, `alpha`
 | | Ubuntu: `16.04-lts`
 | | GCI: `stable`
**user_ssh_keyset** | integer | ID of the SSH keyset that contains the public key to be used to SSH into nodes.
**solutions** | A list of solution objects.

### Solution Attributes

**Name** | **Type** | **Description**
--------- | ---- | -----------
**solution** | string | Solution to be installed. Allowed values are: `autoscaler`, `calico`, `cloudflare-warp-ingress`, `efk`, `gitlab`, `gitlab_ee`, `haproxy`, `helm_tiller`, `istio`, `kubeless`, `linkerd`, `prometheus`, `sysdig`, and `turbonomic`.
**keyset** | integer | ID of the solution keyset to use. Must belong to same organization (and workspace if applicable) as the cluster. Valid only for`turbonomic` and `sysdig` solutions.
**max_nodes** | integer | Number of nodes the autoscaler should scale to. Valid only for `autoscaler`.

## Example: Create an AWS Cluster

> Example request:

```shell
curl -X POST \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-d @create-aws-cluster.json \
https://api.stackpoint.io/orgs/3/clusters
```

> Contents of create-aws-cluster.json:

```json
{
    "name": "My New Cluster",
    "provider": "aws",
    "provider_keyset": 4,
    "master_count": 1,
    "master_size": "t2.large",
    "worker_count": 2,
    "worker_size": "t2.large",
    "region": "us-west-2",
    "zone": "us-west-2a",
    "provider_network_id": "vpc-c4a6f5a0",
    "provider_network_cidr": "172.22.0.0/16",
    "provider_subnet_id": "subnet-d19044b6",
    "provider_subnet_cidr": "172.22.4.0/24",
    "k8s_version": "v1.8.3",
    "k8s_rbac_enabled": true,
    "k8s_dashboard_enabled": true,
    "etcd_type": "self_hosted",
    "platform": "coreos",
    "channel": "stable",
    "user_ssh_keyset": 5,
    "solutions": [
        {
            "solution": "helm_tiller"
        }
    ]
}

```

> Example response:

```json
{
  "pk": 1,
  "name": "My New Cluster",
  "org": 3,
  "site": 8,
  "workspace": {
    "pk": 3,
    "name": "Default",
    "slug": "default",
    "org": 3,
    "is_default": true,
    "created": "2019-02-12T20:11:53.479801Z"
  },
  "instance_id": "spcex8dqlt",
  "provider": "aws",
  "provider_keyset": 4,
  "provider_keyset_name": "My Renamed AWS Keyset2",
  "region": "us-west-2",
  "platform": "coreos",
  "channel": "stable",
  "state": "draft",
  "project_id": "",
  "owner": 3,
  "user_ssh_keyset": 5,
  "user_ssh_keyset_name": "Default SPC SSH Keypair",
  "etcd_type": "self_hosted",
  "provider_network_id": "vpc-c4a6f5a0",
  "provider_network_cidr": "172.22.0.0\/16",
  "provider_subnet_id": "subnet-d19044b6",
  "provider_subnet_cidr": "172.22.4.0\/24",
  "provider_balancer_id": null,
  "provider_resource_group": null,
  "config": {

  },
  "layout": {

  },
  "solutions": [
    {
      "pk": 1,
      "name": "Helm Tiller",
      "instance_id": "solx82p20x",
      "cluster": 1,
      "solution": "helm_tiller",
      "installer": "ansible_custom",
      "keyset": null,
      "keyset_name": "",
      "version": "",
      "version_migrations": [

      ],
      "state": "draft",
      "url": "",
      "username": "",
      "password": "",
      "max_nodes": null,
      "git_repo": "",
      "git_path": "",
      "initial": true,
      "config": {

      },
      "extra_data": {

      },
      "created": "2019-02-13T16:44:20.243883Z",
      "updated": "2019-02-13T16:44:20.244065Z",
      "is_deleteable": false
    }
  ],
  "features": [

  ],
  "follower": {

  },
  "notified": false,
  "created": "2019-02-13T16:44:19.437099Z",
  "updated": "2019-02-13T16:44:20.103316Z",
  "k8s_version": "v1.8.3",
  "k8s_dashboard_enabled": true,
  "k8s_rbac_enabled": true,
  "k8s_etcd_operator_installed": false,
  "k8s_dashboard_installed": false,
  "k8s_pod_cidr": "10.2.0.0\/16",
  "k8s_service_cidr": "10.3.0.0\/24",
  "is_kubeconfig_available": false,
  "kubeconfig_path": "\/orgs\/3\/clusters\/1\/kubeconfig",
  "node_count": 3,
  "master_count": 1,
  "master_size": "t2.large",
  "worker_count": 2,
  "worker_size": "nodepool-dependent",
  "image": "ami-0b0f4f5f0c8c1a797",
  "zone": "us-west-2a",
  "is_k8s_available": false,
  "is_failed": true,
  "federation_role": null,
  "k8s_etcd_cluster": null,
  "is_etcd_host": false,
  "version_migrations": [
    "v1.8.11"
  ],
  "istio_mesh_member": null,
  "owner_detail": "jdoe@example.com"
}
```

Create an AWS cluster with Helm installed as a solution.

## DELETE a Cluster

```shell
curl -X DELETE "https://api.stackpoint.io/orgs/{Org ID}/clusters/{Cluster ID}"
```

> Example request to delete the cluster with Cluster ID 1:

```shell
curl -X DELETE \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
https://api.stackpoint.io/orgs/3/clusters/1
```

> If the cluster is successfully deleted, this command returns an empty response with status code `204`.

Delete the cluster and any associated nodes, solutions and/or volumes.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Cluster ID** | Yes | The Cluster ID.
