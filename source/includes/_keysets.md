# Keysets

Keysets are credentials used by the system to provision clusters, add nodes, or install applications.

Keysets are scoped by organization.

## GET /orgs/{Org ID}/keysets

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/2/keysets"
```

> Example response:

```json
[
  {
    "pk": 1,
    "name": "My AWS Credentials",
    "category": "provider",
    "entity": "aws",
    "org": 2,
    "workspaces": [

    ],
    "user": 1,
    "is_default": false,
    "keys": [
      {
        "pk": 2,
        "keyset": 1,
        "key_type": "pub",
        "fingerprint": "",
        "user": 1
      },
      {
        "pk": 3,
        "keyset": 2,
        "key_type": "pvt",
        "fingerprint": "",
        "user": 1
      }
    ],
    "created": "2018-11-14T22:03:02.892559Z"
  }
]
```

Get all of the Keysets belonging to the specified Organization. Each Keyset contains one or more Keys.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Keyset ID.
**name** | Credential name.
**category** | Keyset category. Options include `provider`, `solution`, `storage`, `VCS`, and `SSH`.
**entity** | Provider name.
**org** | Organization ID.
**workspaces** | The workspace(s) to which the credential is assigned.
**user** | The user to whom the credential is assigned.
**is_default** | Whether the credential is set as "Default" or not.
**keys** | Credentials contained in the keyset.
**keyset** | The Keyset ID to which the credential belongs.
**key_type** | The type of Key.
**fingerprint** | For SSH credentials: The RSA fingerprint.
**created** | Timestamp of the Keyset's create date.

## GET /orgs/{Org ID}/keysets/{Keyset ID}

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/2/keysets/3"
```

> Example response:

```json
{
  "pk": 3,
  "name": "JDoe AWS Credentials",
  "category": "provider",
  "entity": "",
  "org": 2,
  "workspaces": [

  ],
  "user": 3,
  "is_default": false,
  "keys": [

  ],
  "created": "2019-02-06T17:32:05.802960Z"
}
```

Get information for a specific Keyset.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Keyset ID** | Yes | The Keyset ID

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Keyset ID.
**name** | Credential name.
**category** | Keyset category. Options include `provider`, `solution`, `storage`, `VCS`, and `SSH`.
**entity** | The entity to which the Keyset belongs.
**org** | Organization ID.
**workspaces** | The workspace(s) to which the credential is assigned.
**user** | The user to whom the credential is assigned.
**is_default** | Whether the credential is set as "Default" or not.
**keys** | Credentials contained in the keyset.
**keyset** | The Keyset ID to which the credential belongs.
**key_type** | The type of Key.
**fingerprint** | For SSH credentials: The RSA fingerprint.
**created** | Timestamp of the Keyset's create date.

## POST /orgs/{Org ID}/keysets

> Example request: Create an AWS Keyset

```shell
curl -X POST \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-H "Content-Type: application/json" \
-d @create-aws-keyset.json \
"https://api.stackpoint.io/orgs/1/keysets"
```

> Contents of `create-aws-keyset.json`:

```json
{
  "name": "My AWS Keyset",
  "category": "provider",
  "entity": "aws",
  "workspaces": [],
  "keys": [
    {
      "key_type": "pub",
      "key": "123456789aBcDeF"
    },
    {
      "key_type": "pvt",
      "key": "aBcDeF123456789"
    }
  ]
}

```

> Example response:

```json
{
  "pk": 45675,
  "name": "My AWS Keyset",
  "category": "provider",
  "entity": "aws",
  "org": 2,
  "workspaces": [

  ],
  "user": 2,
  "is_default": false,
  "keys": [
    {
      "pk": 3,
      "keyset": 5,
      "key_type": "pvt",
      "fingerprint": "",
      "user": 380
    },
    {
      "pk": 4,
      "keyset": 6,
      "key_type": "pub",
      "fingerprint": "",
      "user": 380
    }
  ],
  "created": "2019-02-07T21:24:43.037968Z"
}
```

Create a new Keyset for the specified organization. Each keyset contains one or more Keys.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.

### Keyset and Key Values

**Name** | **Type** | **Required** | **Description**
---------|----------|--------------|----------------
**name** | string | Yes | The Keyset name. Must be unique within the Organization by category and entity.
**category** | string | Yes | The Keyset category. Allowed values are: `provider`, `solution`, `storage`, `vcs`, `user_ssh`
**entity** | string | No | The entity to which the keyset applies. [See below for more details and allowed values](#keyset-details).
**org** | integer | Yes | The Organization ID.
**workspaces** | list of integers | No | A list of Workspace IDs within the Organization to which the Keyset applies. To enable Organization-wide access, leave this value empty.
**user** | integer | No | The ID of the user to whom the key is assigned.
**is_default** | string | No | Whether or not this is a default credential. Allowed values are `true` and `false`.
**keys** | list of objects | Yes | A list of keys to attach to the Keyset.
**key_type** | string | Yes | Type of key. Varies by keyset category and entity. [See below for more details and allowed values](#keyset-details).
**key** | string | Yes | The content of the key. This value is encrypted before being stored to the database. This value is not returned in GET requests.

### Keyset Details

NOTE: When creating a Keyset, the required number of Keys must be passed.

**Providers**


**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
AKS | X | `X` | XXXX | XXXX
`aws` | 2 | `pub` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-aws.html" target="blank">Access Key ID</a>
 | | `pvt` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-aws.html" target="blank">Secret Access Key</a>
`azure` | 4 | `subscription` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-azure.html">Subscription ID</a>
  | | `tenant` | string | Tenant ID
  | | `pub` | string | Client ID
  | | `pvt` | string | Client Secret
`do` | 1 | `token` | string | API Token
EKS | X | `X` | XXXX | XXXX
`gce` | 1 | `other` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-gce.html">Service Account JSON</a>
`gke` | 1 | `other` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-gke.html">Service Account JSON</a>
Packet | X | `X` | XXXX | XXXX
ProfitBricks | `X` | XXXX | XXXX
1&1 | X | `X` | XXXX | XXXX

**Solutions**

**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
NetApp Cloud Volumes for AWS | X | `X` | XXXX | XXXX
`sysdig` | 1 | `token` | string | Sysdig Cloud Access Key
Tectonic | X | `X` | XXXX | XXXX
`turbonomic` | 4 | `url` | string | Turbonomic Instance URL
 | | `username` | string | Username
 | | `password` | string | Password
 | | `scope` | string | Value must be `external`
Twistlock | X | `X` | XXXX | XXXX

**Storage**

**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
XX | XX | XX | XX | XX

**VCS**

**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
XX | XX | XX | XX | XX

**User SSH**

**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
1 | `pub` | string | SSH Public key

## PATCH /orgs/{Org ID}/keysets/{Keyset ID}

> Example request: Update an AWS Keyset name using a JSON file

```shell
curl -X PATCH \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-H "Content-Type: application/json" \
-d @rename-aws-keyset.json \
"https://api.stackpoint.io/orgs/2/keysets/4"
```

> Contents of `rename-aws-keyset.json`:

```json
{
  "name": "My Renamed AWS Keyset"
}

```

> Alternate example: Update an AWS Keyset name as form data:

```shell
curl -X PATCH \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-H "Content-Type: multipart/form-data" \
-F name="My Renamed AWS Keyset" \
"https://api.stackpoint.io/orgs/2/keysets/4"
```

> Example response:

```json
{
  "pk": 4,
  "name": "My Renamed AWS Keyset2",
  "category": "provider",
  "entity": "aws",
  "org": 2,
  "workspaces": [

  ],
  "user": 3,
  "is_default": false,
  "keys": [
    {
      "pk": 5,
      "keyset": 4,
      "key_type": "pub",
      "fingerprint": "",
      "user": 3
    },
    {
      "pk": 6,
      "keyset": 4,
      "key_type": "pvt",
      "fingerprint": "",
      "user": 3
    }
  ],
  "created": "2019-02-07T21:40:50.675410Z"
}
```

Update information for an existing Keyset.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Keyset ID** | Yes | The Keyset ID

### Keyset and Key Values

**Name** | **Type** | **Required** | **Description**
---------|----------|--------------|----------------
**name** | string | Yes | The Keyset name. Must be unique within the Organization by category and entity.
**category** | string | Yes | The Keyset category. Allowed values are: `provider`, `solution`, `storage`, `vcs`, `user_ssh`
**entity** | string | No | The entity to which the keyset applies. [See below for more details and allowed values](#keyset-details).
**org** | integer | Yes | The Organization ID.
**workspaces** | list of integers | No | A list of Workspace IDs within the Organization to which the Keyset applies. To enable Organization-wide access, leave this value empty.
**user** | integer | No | The ID of the user to whom the key is assigned.
**is_default** | string | No | Whether or not this is a default credential. Allowed values are `true` and `false`.
**keys** | list of objects | Yes | A list of keys to attach to the Keyset.
**key_type** | string | Yes | Type of key. Varies by keyset category and entity. [See below for more details and allowed values](#keyset-details).
**key** | string | Yes | The content of the key. This value is encrypted before being stored to the database. This value is not returned in GET requests.

### Keyset Details

NOTE: When creating a Keyset, the required number of Keys must be passed.

**Providers**


**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
AKS | X | `X` | XXXX | XXXX
`aws` | 2 | `pub` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-aws.html" target="blank">Access Key ID</a>
 | | `pvt` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-aws.html" target="blank">Secret Access Key</a>
`azure` | 4 | `subscription` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-azure.html">Subscription ID</a>
  | | `tenant` | string | Tenant ID
  | | `pub` | string | Client ID
  | | `pvt` | string | Client Secret
`do` | 1 | `token` | string | API Token
EKS | X | `X` | XXXX | XXXX
`gce` | 1 | `other` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-gce.html">Service Account JSON</a>
`gke` | 1 | `other` | string | <a href="https://docs.netapp.com/us-en/kubernetes-service/create-auth-credentials-on-gke.html">Service Account JSON</a>
Packet | X | `X` | XXXX | XXXX
ProfitBricks | `X` | XXXX | XXXX
1&1 | X | `X` | XXXX | XXXX

**Solutions**

**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
NetApp Cloud Volumes for AWS | X | `X` | XXXX | XXXX
`sysdig` | 1 | `token` | string | Sysdig Cloud Access Key
Tectonic | X | `X` | XXXX | XXXX
`turbonomic` | 4 | `url` | string | Turbonomic Instance URL
 | | `username` | string | Username
 | | `password` | string | Password
 | | `scope` | string | Value must be `external`
Twistlock | X | `X` | XXXX | XXXX

**Storage**

**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
XX | XX | XX |
 XX | XX

**VCS**

**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
XX | XX | XX | XX | XX

**User SSH**

**Entity** | **Number of Keys** | **Key Type** | **Data Type** | **Description**
---------- | ------------------ | ------------ | ------------- | ---------------
1 | `pub` | string | SSH Public key

## DELETE /orgs/{Org ID}/keysets/{Keyset ID}

> Example: Delete Keyset ID 3

```shell
curl -X DELETE \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/2/keysets/3"
```

> A successful DELETE returns an empty response with status code `204`

Delete the specified Keyset. All associated keys are removed.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Keyset ID** | Yes | The Keyset ID

<aside class="warning">If you delete a keyset associated with a running cluster, you will not be able to add or remove nodes or delete the cluster cleanly.</aside>
