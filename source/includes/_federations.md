# Federations

Federation simplifies the process of managing multiple clusters, by allowing you to sync resources across clusters, auto-configure DNS servers for cross-cluster discovery, and more.

## GET All Federations

```shell
GET https://api.stackpoint.io/orgs/{Org ID}/federations
```
> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/federations"
```

> Example response:

```json
[
  {
    "pk": 103,
    "identifier": "spc-yunp9s0hn6",
    "name": "Test Federation",
    "org": 132,
    "workspace": {
      "pk": 152,
      "name": "Default",
      "slug": "default-108",
      "org": 132,
      "is_default": true,
      "created": "2018-09-24T21:22:42.752604Z"
    },
    "dns_zone": "example.com.",
    "dns_provider": "google-clouddns",
    "dns_provider_keyset": 4688,
    "state": "running",
    "roles": [
      {
        "pk": 178,
        "federation": 103,
        "cluster": {
          "pk": 6173,
          "instance_id": "netpsu50lk",
          "name": "Test 2",
          "org": 132,
          "provider": "gke",
          "workspace": {
            "pk": 152,
            "name": "Default",
            "slug": "default-108",
            "org": 132,
            "is_default": true,
            "created": "2018-09-24T21:22:42.752604Z"
          },
          "k8s_version": "latest",
          "node_count": 3,
          "etcd_type": "classic",
          "platform": "gci",
          "channel": "stable",
          "region": "us-west1-b",
          "zone": "",
          "state": "running",
          "nodes": [
            {
              "pk": 19659,
              "pool": null,
              "pool_name": "",
              "instance_id": "netpsu50lk-master-1",
              "provider_node_id": "GKE.104.196.240.169",
              "role": "master",
              "private_ip": "not-available",
              "public_ip": "104.196.240.169",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "not-available",
              "state": "running",
              "is_failed": false
            },
            {
              "pk": 19660,
              "pool": 4699,
              "pool_name": "Default Worker Pool",
              "instance_id": "gke-netpsu50lk-default-pool-e9421c44-01xh",
              "provider_node_id": "gke-netpsu50lk-default-pool-e9421c44-01xh",
              "role": "worker",
              "private_ip": "10.138.0.24",
              "public_ip": "35.197.55.187",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "n1-standard-1",
              "state": "missing",
              "is_failed": false
            },
            {
              "pk": 19661,
              "pool": 4699,
              "pool_name": "Default Worker Pool",
              "instance_id": "gke-netpsu50lk-default-pool-e9421c44-w3cl",
              "provider_node_id": "gke-netpsu50lk-default-pool-e9421c44-w3cl",
              "role": "worker",
              "private_ip": "10.138.0.23",
              "public_ip": "35.247.84.96",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "n1-standard-1",
              "state": "missing",
              "is_failed": false
            }
          ],
          "solutions": [
            {
              "pk": 10148,
              "name": "Helm Tiller",
              "solution": "helm_tiller",
              "state": "installed",
              "initial": true,
              "config": {

              }
            }
          ],
          "is_failed": false,
          "federation_role": "guest",
          "version_migrations": [

          ],
          "k8s_rbac_enabled": true,
          "created": "2019-03-26T16:57:58.133657Z"
        },
        "role": "guest",
        "state": "joining",
        "created": "2019-03-26T17:16:32.131167Z",
        "updated": "2019-03-26T17:20:31.833048Z"
      },
      {
        "pk": 179,
        "federation": 103,
        "cluster": {
          "pk": 6172,
          "instance_id": "net4n5h7cc",
          "name": "Test 1",
          "org": 132,
          "provider": "gke",
          "workspace": {
            "pk": 152,
            "name": "Default",
            "slug": "default-108",
            "org": 132,
            "is_default": true,
            "created": "2018-09-24T21:22:42.752604Z"
          },
          "k8s_version": "latest",
          "node_count": 3,
          "etcd_type": "classic",
          "platform": "gci",
          "channel": "stable",
          "region": "us-west1-b",
          "zone": "",
          "state": "running",
          "nodes": [
            {
              "pk": 19656,
              "pool": null,
              "pool_name": "",
              "instance_id": "net4n5h7cc-master-1",
              "provider_node_id": "GKE.35.199.187.13",
              "role": "master",
              "private_ip": "not-available",
              "public_ip": "35.199.187.13",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "not-available",
              "state": "running",
              "is_failed": false
            },
            {
              "pk": 19657,
              "pool": 4698,
              "pool_name": "Default Worker Pool",
              "instance_id": "gke-net4n5h7cc-default-pool-d81d40f6-c2m7",
              "provider_node_id": "gke-net4n5h7cc-default-pool-d81d40f6-c2m7",
              "role": "worker",
              "private_ip": "10.138.0.21",
              "public_ip": "35.247.98.143",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "n1-standard-1",
              "state": "missing",
              "is_failed": false
            },
            {
              "pk": 19658,
              "pool": 4698,
              "pool_name": "Default Worker Pool",
              "instance_id": "gke-net4n5h7cc-default-pool-d81d40f6-fw08",
              "provider_node_id": "gke-net4n5h7cc-default-pool-d81d40f6-fw08",
              "role": "worker",
              "private_ip": "10.138.0.22",
              "public_ip": "35.197.109.241",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "n1-standard-1",
              "state": "missing",
              "is_failed": false
            }
          ],
          "solutions": [
            {
              "pk": 10147,
              "name": "Helm Tiller",
              "solution": "helm_tiller",
              "state": "installed",
              "initial": true,
              "config": {

              }
            }
          ],
          "is_failed": false,
          "federation_role": "host",
          "version_migrations": [

          ],
          "k8s_rbac_enabled": true,
          "created": "2019-03-26T16:57:34.093914Z"
        },
        "role": "host",
        "state": "joined",
        "created": "2019-03-26T17:16:32.138101Z",
        "updated": "2019-03-26T17:20:31.119184Z"
      }
    ],
    "is_kubeconfig_available": true,
    "etcd_operator": null,
    "deployments": [

    ],
    "created": "2019-03-26T17:16:32.120793Z",
    "updated": "2019-03-26T17:16:32.496470Z"
  }
]
```

Get all Federations belonging to the specified Organization.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.


### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Federation ID.
**identifier** | An internal ID used to identify the Federation.
**name** | The Federation's name.
**org** | The Organization ID.
**workspace** | Workspace details.
**pk** | Workspace ID.
**name** | Workspace name.
**slug** | A human-readable unique identifier, used for storing Workspace data.
**org** | The Organization ID.
**is_default** | Whether or not this is the default Workspace.
**created** | The Workspace creation timestamp.
**dns_zone** | The domain name specified for the Federation.
**dns_provider** | The Federation's DNS provider.
**dns_provider_keyset** | The DNS provider's Keyset ID.
**state** | The Federation's current state.
**roles** | Details for each cluster in the Federation.
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
**federation_role** | The cluster's role in the federation, either `host` or `guest`.
**k8s_rbac_enabled** | Whether or not the cluster has RBAC enabled.
**is_kubeconfig_available** | Whether or not the Federation's kubeconfig file is available for download.
**etcd_operator** | ID of the etcd Operator, if applicable. This value is `null` if there is no etcd Operator.
**deployments** | Deployment details, if applicable. This array is empty if there are no deployments.
**created** | Timestamp of the Federation's creation.
**updated** | Timestamp of the Federation's last modification.

## GET a Specific Federation

```shell
GET https://api.stackpoint.io/orgs/{Org ID}/federations/{Federation ID}
```
> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/federations/103"
```

> Example response:

```json
[
  {
    "pk": 103,
    "identifier": "spc-yunp9s0hn6",
    "name": "Test Federation",
    "org": 132,
    "workspace": {
      "pk": 152,
      "name": "Default",
      "slug": "default-108",
      "org": 132,
      "is_default": true,
      "created": "2018-09-24T21:22:42.752604Z"
    },
    "dns_zone": "example.com.",
    "dns_provider": "google-clouddns",
    "dns_provider_keyset": 4688,
    "state": "running",
    "roles": [
      {
        "pk": 178,
        "federation": 103,
        "cluster": {
          "pk": 6173,
          "instance_id": "netpsu50lk",
          "name": "Test 2",
          "org": 132,
          "provider": "gke",
          "workspace": {
            "pk": 152,
            "name": "Default",
            "slug": "default-108",
            "org": 132,
            "is_default": true,
            "created": "2018-09-24T21:22:42.752604Z"
          },
          "k8s_version": "latest",
          "node_count": 3,
          "etcd_type": "classic",
          "platform": "gci",
          "channel": "stable",
          "region": "us-west1-b",
          "zone": "",
          "state": "running",
          "nodes": [
            {
              "pk": 19659,
              "pool": null,
              "pool_name": "",
              "instance_id": "netpsu50lk-master-1",
              "provider_node_id": "GKE.104.196.240.169",
              "role": "master",
              "private_ip": "not-available",
              "public_ip": "104.196.240.169",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "not-available",
              "state": "running",
              "is_failed": false
            },
            {
              "pk": 19660,
              "pool": 4699,
              "pool_name": "Default Worker Pool",
              "instance_id": "gke-netpsu50lk-default-pool-e9421c44-01xh",
              "provider_node_id": "gke-netpsu50lk-default-pool-e9421c44-01xh",
              "role": "worker",
              "private_ip": "10.138.0.24",
              "public_ip": "35.197.55.187",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "n1-standard-1",
              "state": "missing",
              "is_failed": false
            },
            {
              "pk": 19661,
              "pool": 4699,
              "pool_name": "Default Worker Pool",
              "instance_id": "gke-netpsu50lk-default-pool-e9421c44-w3cl",
              "provider_node_id": "gke-netpsu50lk-default-pool-e9421c44-w3cl",
              "role": "worker",
              "private_ip": "10.138.0.23",
              "public_ip": "35.247.84.96",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "n1-standard-1",
              "state": "missing",
              "is_failed": false
            }
          ],
          "solutions": [
            {
              "pk": 10148,
              "name": "Helm Tiller",
              "solution": "helm_tiller",
              "state": "installed",
              "initial": true,
              "config": {

              }
            }
          ],
          "is_failed": false,
          "federation_role": "guest",
          "version_migrations": [

          ],
          "k8s_rbac_enabled": true,
          "created": "2019-03-26T16:57:58.133657Z"
        },
        "role": "guest",
        "state": "joining",
        "created": "2019-03-26T17:16:32.131167Z",
        "updated": "2019-03-26T17:20:31.833048Z"
      },
      {
        "pk": 179,
        "federation": 103,
        "cluster": {
          "pk": 6172,
          "instance_id": "net4n5h7cc",
          "name": "Test 1",
          "org": 132,
          "provider": "gke",
          "workspace": {
            "pk": 152,
            "name": "Default",
            "slug": "default-108",
            "org": 132,
            "is_default": true,
            "created": "2018-09-24T21:22:42.752604Z"
          },
          "k8s_version": "latest",
          "node_count": 3,
          "etcd_type": "classic",
          "platform": "gci",
          "channel": "stable",
          "region": "us-west1-b",
          "zone": "",
          "state": "running",
          "nodes": [
            {
              "pk": 19656,
              "pool": null,
              "pool_name": "",
              "instance_id": "net4n5h7cc-master-1",
              "provider_node_id": "GKE.35.199.187.13",
              "role": "master",
              "private_ip": "not-available",
              "public_ip": "35.199.187.13",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "not-available",
              "state": "running",
              "is_failed": false
            },
            {
              "pk": 19657,
              "pool": 4698,
              "pool_name": "Default Worker Pool",
              "instance_id": "gke-net4n5h7cc-default-pool-d81d40f6-c2m7",
              "provider_node_id": "gke-net4n5h7cc-default-pool-d81d40f6-c2m7",
              "role": "worker",
              "private_ip": "10.138.0.21",
              "public_ip": "35.247.98.143",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "n1-standard-1",
              "state": "missing",
              "is_failed": false
            },
            {
              "pk": 19658,
              "pool": 4698,
              "pool_name": "Default Worker Pool",
              "instance_id": "gke-net4n5h7cc-default-pool-d81d40f6-fw08",
              "provider_node_id": "gke-net4n5h7cc-default-pool-d81d40f6-fw08",
              "role": "worker",
              "private_ip": "10.138.0.22",
              "public_ip": "35.197.109.241",
              "root_disk_size": null,
              "gpu_instance_size": "",
              "gpu_core_count": null,
              "zone": "",
              "size": "n1-standard-1",
              "state": "missing",
              "is_failed": false
            }
          ],
          "solutions": [
            {
              "pk": 10147,
              "name": "Helm Tiller",
              "solution": "helm_tiller",
              "state": "installed",
              "initial": true,
              "config": {

              }
            }
          ],
          "is_failed": false,
          "federation_role": "host",
          "version_migrations": [

          ],
          "k8s_rbac_enabled": true,
          "created": "2019-03-26T16:57:34.093914Z"
        },
        "role": "host",
        "state": "joined",
        "created": "2019-03-26T17:16:32.138101Z",
        "updated": "2019-03-26T17:20:31.119184Z"
      }
    ],
    "is_kubeconfig_available": true,
    "etcd_operator": null,
    "deployments": [

    ],
    "created": "2019-03-26T17:16:32.120793Z",
    "updated": "2019-03-26T17:16:32.496470Z"
  }
]
```

Get the details of the specified Federation.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Federation ID** | Yes | The Federation ID.


### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Federation ID.
**identifier** | An internal ID used to identify the Federation.
**name** | The Federation's name.
**org** | The Organization ID.
**workspace** | Workspace details.
**pk** | Workspace ID.
**name** | Workspace name.
**slug** | A human-readable unique identifier, used for storing Workspace data.
**org** | The Organization ID.
**is_default** | Whether or not this is the default Workspace.
**created** | The Workspace creation timestamp.
**dns_zone** | The domain name specified for the Federation.
**dns_provider** | The Federation's DNS provider.
**dns_provider_keyset** | The DNS provider's Keyset ID.
**state** | The Federation's current state.
**roles** | Details for each cluster in the Federation.
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
**federation_role** | The cluster's role in the federation, either `host` or `guest`.
**k8s_rbac_enabled** | Whether or not the cluster has RBAC enabled.
**is_kubeconfig_available** | Whether or not the Federation's kubeconfig file is available for download.
**etcd_operator** | ID of the etcd Operator, if applicable. This value is `null` if there is no etcd Operator.
**deployments** | Deployment details, if applicable. This array is empty if there are no deployments.
**created** | Timestamp of the Federation's creation.
**updated** | Timestamp of the Federation's last modification.

## POST Add a Guest Cluster to a Federation

```shell
POST https://api.stackpoint.io/orgs/{Org ID}/federations/{Federation ID}/roles
```
> Example request:

```shell
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-d @add-guest.json \
"https://api.stackpoint.io/orgs/3/federations/103/roles"
```

> Contents of `add-guest.json`. Replace `12` with the ID of the cluster you want to add to the Federation:

```shell
{
  "cluster": "12",
  "role": "guest"
}
```

> Example response. If the cluster is added successfully, the API server will respond with the details of the newly-added cluster. As further confirmation that the cluster has been successfully added, note that `federation_role` is returned as `guest`:

```json
[
  {
    "pk": 181,
    "federation": 103,
    "cluster": {
      "pk": 12,
      "instance_id": "netlc8pqot",
      "name": "Test 4",
      "org": 132,
      "provider": "gke",
      "workspace": {
        "pk": 152,
        "name": "Default",
        "slug": "default-108",
        "org": 132,
        "is_default": true,
        "created": "2018-09-24T21:22:42.752604Z"
      },
      "k8s_version": "latest",
      "node_count": 3,
      "etcd_type": "classic",
      "platform": "gci",
      "channel": "stable",
      "region": "us-west1-b",
      "zone": "",
      "state": "running",
      "nodes": [
        {
          "pk": 19665,
          "pool": null,
          "pool_name": "",
          "instance_id": "netlc8pqot-master-1",
          "provider_node_id": "GKE.104.196.234.209",
          "role": "master",
          "private_ip": "not-available",
          "public_ip": "104.196.234.209",
          "root_disk_size": null,
          "gpu_instance_size": "",
          "gpu_core_count": null,
          "zone": "",
          "size": "not-available",
          "state": "running",
          "is_failed": false
        },
        {
          "pk": 19666,
          "pool": 4701,
          "pool_name": "Default Worker Pool",
          "instance_id": "gke-netlc8pqot-default-pool-88114825-gqzj",
          "provider_node_id": "gke-netlc8pqot-default-pool-88114825-gqzj",
          "role": "worker",
          "private_ip": "10.138.0.27",
          "public_ip": "35.233.164.152",
          "root_disk_size": null,
          "gpu_instance_size": "",
          "gpu_core_count": null,
          "zone": "",
          "size": "n1-standard-1",
          "state": "missing",
          "is_failed": false
        },
        {
          "pk": 19667,
          "pool": 4701,
          "pool_name": "Default Worker Pool",
          "instance_id": "gke-netlc8pqot-default-pool-88114825-m9zc",
          "provider_node_id": "gke-netlc8pqot-default-pool-88114825-m9zc",
          "role": "worker",
          "private_ip": "10.138.0.32",
          "public_ip": "35.230.96.0",
          "root_disk_size": null,
          "gpu_instance_size": "",
          "gpu_core_count": null,
          "zone": "",
          "size": "n1-standard-1",
          "state": "missing",
          "is_failed": false
        }
      ],
      "solutions": [
        {
          "pk": 10150,
          "name": "Helm Tiller",
          "solution": "helm_tiller",
          "state": "installed",
          "initial": true,
          "config": {

          }
        }
      ],
      "is_failed": false,
      "federation_role": "guest",
      "version_migrations": [

      ],
      "k8s_rbac_enabled": true,
      "created": "2019-03-26T17:37:49.671542Z"
    },
    "role": "guest",
    "state": "draft",
    "created": "2019-03-26T17:54:55.789593Z",
    "updated": "2019-03-26T17:54:55.789613Z"
  }
]
```

Add a guest cluster to an existing Federation.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Federation ID* | Yes | The Federation ID.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Federation ID.
**identifier** | An internal ID used to identify the Federation.
**name** | The Federation's name.
**org** | The Organization ID.
**workspace** | Workspace details.
**pk** | Workspace ID.
**name** | Workspace name.
**slug** | A human-readable unique identifier, used for storing Workspace data.
**org** | The Organization ID.
**is_default** | Whether or not this is the default Workspace.
**created** | The Workspace creation timestamp.
**dns_zone** | The domain name specified for the Federation.
**dns_provider** | The Federation's DNS provider.
**dns_provider_keyset** | The DNS provider's Keyset ID.
**state** | The Federation's current state.
**roles** | Details for each cluster in the Federation.
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
**federation_role** | The cluster's role in the federation, either `host` or `guest`.
**k8s_rbac_enabled** | Whether or not the cluster has RBAC enabled.
**is_kubeconfig_available** | Whether or not the Federation's kubeconfig file is available for download.
**etcd_operator** | ID of the etcd Operator, if applicable. This value is `null` if there is no etcd Operator.
**deployments** | Deployment details, if applicable. This array is empty if there are no deployments.
**created** | Timestamp of the Federation's creation.
**updated** | Timestamp of the Federation's last modification.

## POST Create a New Federation


```shell
POST https://api.stackpoint.io/orgs/{Org ID}/workspaces/{Workspace ID}/federations
```

> Example request

```shell
curl -X POST \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-H "Content-Type: application/json" \
-d @create-aws-federation.json \
"https://api.stackpoint.io/orgs/1/workspaces/11/federations"
```

> Contents of create-federation.json. Replace the values as specified below. Be sure to specify the `role` for one cluster as `host`, and the rest as `guest`. The host cluster cannot be changed after the Federation has been created.

```json
{
  "name": "My New Federation",
  "workspace": 15,
  "dns_zone": "example.com.",
  "dns_provider": "google-clouddns",
  "dns_provider_keyset": 12,
  "roles": [
    {
      "cluster": 1,
      "role": "guest"
    },
    {
      "cluster": 2,
      "role": "host"
    }
  ],
  "deployments": [

  ]
}
```

> Example response:

```json
{
  "pk": 106,
  "identifier": "spc-shyaz3pp13",
  "name": "Another Erika API Test Federation",
  "org": 132,
  "workspace": {
    "pk": 152,
    "name": "Default",
    "slug": "default-108",
    "org": 132,
    "is_default": true,
    "created": "2018-09-24T21:22:42.752604Z"
  },
  "dns_zone": "example.com.",
  "dns_provider": "google-clouddns",
  "dns_provider_keyset": 4688,
  "state": "draft",
  "roles": [
    {
      "pk": 188,
      "federation": 106,
      "cluster": {
        "pk": 6175,
        "instance_id": "netlc8pqot",
        "name": "Erika API Test 4",
        "org": 132,
        "provider": "gke",
        "workspace": {
          "pk": 152,
          "name": "Default",
          "slug": "default-108",
          "org": 132,
          "is_default": true,
          "created": "2018-09-24T21:22:42.752604Z"
        },
        "k8s_version": "latest",
        "node_count": 3,
        "etcd_type": "classic",
        "platform": "gci",
        "channel": "stable",
        "region": "us-west1-b",
        "zone": "",
        "state": "running",
        "nodes": [
          {
            "pk": 19665,
            "pool": null,
            "pool_name": "",
            "instance_id": "netlc8pqot-master-1",
            "provider_node_id": "GKE.104.196.234.209",
            "role": "master",
            "private_ip": "not-available",
            "public_ip": "104.196.234.209",
            "root_disk_size": null,
            "gpu_instance_size": "",
            "gpu_core_count": null,
            "zone": "",
            "size": "not-available",
            "state": "running",
            "is_failed": false
          },
          {
            "pk": 19666,
            "pool": 4701,
            "pool_name": "Default Worker Pool",
            "instance_id": "gke-netlc8pqot-default-pool-88114825-gqzj",
            "provider_node_id": "gke-netlc8pqot-default-pool-88114825-gqzj",
            "role": "worker",
            "private_ip": "10.138.0.27",
            "public_ip": "35.233.164.152",
            "root_disk_size": null,
            "gpu_instance_size": "",
            "gpu_core_count": null,
            "zone": "",
            "size": "n1-standard-1",
            "state": "missing",
            "is_failed": false
          },
          {
            "pk": 19667,
            "pool": 4701,
            "pool_name": "Default Worker Pool",
            "instance_id": "gke-netlc8pqot-default-pool-88114825-m9zc",
            "provider_node_id": "gke-netlc8pqot-default-pool-88114825-m9zc",
            "role": "worker",
            "private_ip": "10.138.0.32",
            "public_ip": "35.230.96.0",
            "root_disk_size": null,
            "gpu_instance_size": "",
            "gpu_core_count": null,
            "zone": "",
            "size": "n1-standard-1",
            "state": "missing",
            "is_failed": false
          }
        ],
        "solutions": [
          {
            "pk": 10150,
            "name": "Helm Tiller",
            "solution": "helm_tiller",
            "state": "installed",
            "initial": true,
            "config": {

            }
          }
        ],
        "is_failed": false,
        "federation_role": "guest",
        "version_migrations": [

        ],
        "k8s_rbac_enabled": true,
        "created": "2019-03-26T17:37:49.671542Z"
      },
      "role": "guest",
      "state": "draft",
      "created": "2019-03-26T18:25:42.738461Z",
      "updated": "2019-03-26T18:25:42.738483Z"
    },
    {
      "pk": 189,
      "federation": 106,
      "cluster": {
        "pk": 6174,
        "instance_id": "netrg5st5g",
        "name": "Erika API Test 3",
        "org": 132,
        "provider": "gke",
        "workspace": {
          "pk": 152,
          "name": "Default",
          "slug": "default-108",
          "org": 132,
          "is_default": true,
          "created": "2018-09-24T21:22:42.752604Z"
        },
        "k8s_version": "latest",
        "node_count": 3,
        "etcd_type": "classic",
        "platform": "gci",
        "channel": "stable",
        "region": "us-west1-b",
        "zone": "",
        "state": "running",
        "nodes": [
          {
            "pk": 19662,
            "pool": null,
            "pool_name": "",
            "instance_id": "netrg5st5g-master-1",
            "provider_node_id": "GKE.35.230.16.53",
            "role": "master",
            "private_ip": "not-available",
            "public_ip": "35.230.16.53",
            "root_disk_size": null,
            "gpu_instance_size": "",
            "gpu_core_count": null,
            "zone": "",
            "size": "not-available",
            "state": "running",
            "is_failed": false
          },
          {
            "pk": 19663,
            "pool": 4700,
            "pool_name": "Default Worker Pool",
            "instance_id": "gke-netrg5st5g-default-pool-1a1c6a27-5c5j",
            "provider_node_id": "gke-netrg5st5g-default-pool-1a1c6a27-5c5j",
            "role": "worker",
            "private_ip": "10.138.0.25",
            "public_ip": "35.233.167.222",
            "root_disk_size": null,
            "gpu_instance_size": "",
            "gpu_core_count": null,
            "zone": "",
            "size": "n1-standard-1",
            "state": "missing",
            "is_failed": false
          },
          {
            "pk": 19664,
            "pool": 4700,
            "pool_name": "Default Worker Pool",
            "instance_id": "gke-netrg5st5g-default-pool-1a1c6a27-vgw8",
            "provider_node_id": "gke-netrg5st5g-default-pool-1a1c6a27-vgw8",
            "role": "worker",
            "private_ip": "10.138.0.26",
            "public_ip": "35.203.147.167",
            "root_disk_size": null,
            "gpu_instance_size": "",
            "gpu_core_count": null,
            "zone": "",
            "size": "n1-standard-1",
            "state": "missing",
            "is_failed": false
          }
        ],
        "solutions": [
          {
            "pk": 10149,
            "name": "Helm Tiller",
            "solution": "helm_tiller",
            "state": "installed",
            "initial": true,
            "config": {

            }
          }
        ],
        "is_failed": false,
        "federation_role": "host",
        "version_migrations": [

        ],
        "k8s_rbac_enabled": true,
        "created": "2019-03-26T17:37:23.797422Z"
      },
      "role": "host",
      "state": "draft",
      "created": "2019-03-26T18:25:42.745434Z",
      "updated": "2019-03-26T18:25:42.745455Z"
    }
  ],
  "is_kubeconfig_available": false,
  "etcd_operator": null,
  "deployments": [

  ],
  "created": "2019-03-26T18:25:42.734139Z",
  "updated": "2019-03-26T18:25:42.734163Z"
}
```

Create a new Federation with the specified clusters.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Workspace ID** | Yes | The Workspace ID.

### Federation Values

**Name** | **Type** | **Required** | **Description**
---------|----------|--------------|----------------
**name** | string | Yes | The Federation name. Must be unique within the Workspace.
**workspace** | string | Yes | The Workspace ID.
**dns_zone** | string | Yes | The domain name for the Federation.
**dns_provider** | string | Yes | The DNS provider. Allowed values are `google-clouddns` or `aws-route53`.
**dns_provider_keyset** | string | Yes | The DNS provider Keyset ID.
**cluster** | string | Yes | The Cluster ID.
**role** | string | Yes | The Cluster's role in the Federation. Allowed values are `host` or `guest`. One cluster must be assigned the role of `host`. Assign all other clusters the role of `guest`. The host cluster cannot be changed after the Federation has been created.
**deployments** | string | No | Details for any deployments.


### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Federation ID.
**identifier** | An internal ID used to identify the Federation.
**name** | The Federation's name.
**org** | The Organization ID.
**workspace** | Workspace details.
**pk** | Workspace ID.
**name** | Workspace name.
**slug** | A human-readable unique identifier, used for storing Workspace data.
**org** | The Organization ID.
**is_default** | Whether or not this is the default Workspace.
**created** | The Workspace creation timestamp.
**dns_zone** | The domain name specified for the Federation.
**dns_provider** | The Federation's DNS provider.
**dns_provider_keyset** | The DNS provider's Keyset ID.
**state** | The Federation's current state.
**roles** | Details for each cluster in the Federation.
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
**federation_role** | The cluster's role in the federation, either `host` or `guest`.
**k8s_rbac_enabled** | Whether or not the cluster has RBAC enabled.
**is_kubeconfig_available** | Whether or not the Federation's kubeconfig file is available for download.
**etcd_operator** | ID of the etcd Operator, if applicable. This value is `null` if there is no etcd Operator.
**deployments** | Deployment details, if applicable. This array is empty if there are no deployments.
**created** | Timestamp of the Federation's creation.
**updated** | Timestamp of the Federation's last modification.

## DELETE Disband a Federation

```shell
DELETE https://api.stackpoint.io/orgs/{Org ID}/federations/{Federation ID}
```
> Example request:

```shell
curl -X DELETE \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/federations/103"
```

> A successful DELETE returns an empty response with status code `204`

Disband the specified Federation. The host and guest clusters will be detached from the federation but won't be deleted.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Federation ID** | Yes | The Workspace ID.
