# Keysets

Keysets are credentials used by the system to provision clusters, add nodes or install applications.

Keysets are scoped by organization.

## Get All Keysets

```shell
curl "https://api.stackpoint.io/orgs/<ORG_ID>/keysets"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
[
  {
    "pk": 25,
    "name": "My DO Keyset",
    "category": "provider",
    "entity": "do",
    "org": 1,
    "workspaces": [],
    "user": 1,
    "is_default": false,
    "keys": [
      {
        "pk": 30,
        "keyset": 25,
        "key_type": "token",
        "fingerprint": "",
        "user": 1
      }
    ],
    "created": "2016-08-16T23:22:53.490803Z"
  },
  {
    "pk": 26,
    "name": "My AWS Keyset",
    "category": "provider",
    "entity": "aws",
    "org": 1,
    "workspaces": [],
    "user": 1,
    "is_default": false,
    "keys": [
      {
        "pk": 31,
        "keyset": 26,
        "key_type": "pub",
        "fingerprint": "",
        "user": 1
      },
      {
        "pk": 32,
        "keyset": 26,
        "key_type": "pvt",
        "fingerprint": "",
        "user": 1
      }
    ],
    "created": "2016-08-16T23:22:53.490803Z"
  }
]
```

This endpoint retrieves all keysets available to under a specific organization.

The `pk` attribute in the response denotes the keyset ID.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ORG_ID>/keysets`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization

## Get a Specific Keyset

```shell
curl "https://api.stackpoint.io/orgs/1/keysets/25"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
{
  "pk": 25,
  "name": "My DO Keyset",
  "category": "provider",
  "entity": "do",
  "org": 1,
  "workspaces": [],
  "user": 1,
  "is_default": false,
  "keys": [
    {
      "pk": 30,
      "keyset": 25,
      "key_type": "token",
      "fingerprint": "",
      "user": 1
    }
  ],
  "created": "2016-08-16T23:22:53.490803Z"
}
```

This endpoint retrieves a specific keyset.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ORG_ID>/keysets/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
ID | ID of the keyset

## Create a Keyset

There are 3 categories of keysets that can be created using the API.

1. Provider keysets
2. Solution keysets
3. SSH Keyset

Each keyset contains one or more Keys.

### Request Data Attributes

#### Keyset Attributes

Parameter | Type | Description
--------- | ---- | -----------
name | string | Name of the keyset, must be unique by category and entity within an organization
category | string | Category of keyset. Options are: `provider`, `solution`, `user_ssh`
entity | string | Specific entity the keyset applies to, differs by category:
 | | For `provider` category the options are: AWS: `aws`, Azure: `azure`, DigitalOcean: `do`, GCE: `gce`, GKE: `gke`
 | | For `solution` category the options are: Sysdig Cloud: `sysdig`, Turbonomic: `turbonomic`
 | | For `user_ssh` category leave this value empty
workspaces | list of integer | A list of IDs for workspaces within the organization to which the keyset will be restricted to. Leave empty to allow organization wide access
keys | list of objects | A list of keys to attach to keyset

#### Key Attributes

Parameter | Type | Description
--------- | ---- | -----------
key_type | string | Type of key. Varies by keyset category and entity
key | string | Value stored in the key. Encrypted before storing to DB. Value not returned in GET requests

#### List of Key Types and Keys for Providers

When creating a keyset the required # of keys must be passed.

Entity | # of Keys | Key Type | Data Type | Key
------ | --------- | -------- | --------- | ---
`aws` | 2 | `pub` | string | <a href="https://stackpointcloud.com/community/tutorial/how-to-create-auth-credentials-on-amazon-web-services-aws" target="_blank">Access Key ID</a>
 | | `pvt` | string | Secret Access Key
`azure` | 4 | `subscription` | string | <a href="https://stackpointcloud.com/community/tutorial/how-to-create-auth-credentials-on-azure" target="_blank">Subscription ID</a>
 | | `tenant` | string | Tenant ID
 | | `pub` | string | Client ID
 | | `pvt` | string | Client Secret
`do` | 1 | `token` | string | API Token
`gce` | 1 | `other` | string | <a href="https://stackpointcloud.com/community/tutorial/google-compute-engine-setup-and-authentication" target="_blank">Service Account JSON</a>
`gke` | 1 | `other` | string | <a href="https://stackpointcloud.com/community/tutorial/how-to-create-auth-credentials-on-google-container-engine-gke" target="_blank">Service Account JSON</a>

#### List of Key Types and Keys for Solutions

Entity | # of Keys | Key Type | Data Type | Key
------ | --------- | -------- | --------- | ---
`sysdig` | 1 | `token` | string | Sysdig Cloud Access Key
`turbonomic` | 4 | `url` | string | Turbonomic Instance URL
 | | `username` | string | Username
 | | `password` | string | Password
 | | `scope` | string | Value must be `external`

#### List of Key Types and Keys for SSH
\# of Keys | Key Type | Data Type | Key
--------- | -------- | --------- | ---
1 | `pub` | string | SSH Public key


## Create AWS Keyset

```shell
curl --header "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5" \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --request POST \
     --data @create_aws_keyset.json \
     https://api.stackpoint.io/orgs/1/keysets
```

> `create_aws_keyset.json` should contain the following data:

```json
{
  "name": "My AWS Keyset",
  "category": "provider",
  "entity": "aws",
  "workspaces": [],
  "keys": [
    {
      "key_type": "pub",
      "key": "AKIAIXH7J9KGB56VWZGA"
    },
    {
      "key_type": "pvt",
      "key": "FfgssHsds9u3rfsjOHDsssy8w3ehdsokFDDrR"
    }
  ]
}
```

Create an AWS keyset by sending the appropriate keys.

### HTTP Request

`POST https://api.stackpoint.io/orgs/<ORG_ID>/keysets`

### URL Parameters

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization

## Delete a Keyset

```shell
curl -X DELETE "https://api.stackpoint.io/orgs/1/keysets/25"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns an empty response with status code `204`

This endpoint deletes a specific keyset. All associated keys are removed.

### HTTP Request

`DELETE https://api.stackpoint.io/orgs/<ORG_ID>/keysets/<ID>`

Parameter | Description
--------- | -----------
ORG_ID | ID of the organization
ID | ID of the keyset

<aside class="warning">If you remove a provider keyset that is associated with a running cluster, then you will no longer be able to add or remove nodes or delete the cluster cleanly.</aside>
