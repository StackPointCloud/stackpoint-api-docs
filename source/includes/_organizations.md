# Organizations

## Overview

Organizations are the highest-level resource. The Organizations resource contains information about the Organization. This includes the ID, which is required for most other API calls.

### Background

The first time you log in to Stackpoint.io, we automatically create an Organization for you. You can customize the name and logo of this Organization on the [Organization Setup](https://stackpoint.io/organization/setup) page.

## GET All Organizations

```shell
GET https://api.stackpoint.io/orgs/
```

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs"
```

> Example response:

```json
[
  {
    "pk": 2,
    "name": "Company Organization",
    "slug": "company-organization",
    "logo": null,
    "created": "2018-09-24T18:23:22.889260Z",
    "updated": "2018-09-24T18:23:22.889291Z"
  },
  {
    "pk": 1,
    "name": "My Organization",
    "slug": "my-organization",
    "logo": null,
    "created": "2018-08-05T14:35:53.161852Z",
    "updated": "2019-01-31T18:31:21.583756Z"
  }
]
```

Get the list of Organizations of which the user is a member.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Organization ID.
**name** | Organization name.
**slug** | A human-readable unique identifier, used for storing Organization data.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization

## GET a Specific Organization

```shell
GET https://api.stackpoint.io/orgs/{Org ID}
```

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/2"
```

> Example response:

```json
{
  "pk": 2,
  "name": "My Organization",
  "slug": "my-organization",
  "logo": null,
  "created": "2016-08-05T14:35:53.161852Z",
  "updated": "2019-01-31T18:31:21.583756Z"
}
```

Get information for a specific Organization.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.


### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Organization ID.
**name** | Organization name.
**slug** | A human-readable unique identifier, used for storing Organization data.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization

## POST a New Organization

```shell
POST https://api.stackpoint.io/orgs/
```

> Example Request:

```shell
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-d @postorg.json \
"https://api.stackpoint.io/orgs"
```

> Contents of `postorg.json`:

```shell
{
  "name": "My New Organization"
}
```

>  Example Response. If the new Organization is created successfully, the API will return a list of all Organizations of which the user is a member, including the newly-created Organization. The new Organization is listed first.

```json
[
 {
    "pk": 2,
    "name": "My New Organization",
    "slug": "my-new-organization",
    "logo": null,
    "created": "2019-01-31T20:32:01.041059Z",
    "updated": "2019-01-31T20:32:01.041093Z"
},
  {
    "pk": 1,
    "name": "My Organization",
    "slug": "my-organization",
    "logo": null,
    "created": "2018-08-05T14:35:53.161852Z",
    "updated": "2019-01-31T18:31:21.583756Z"
  }
]
```

Create a new Organization in the user's account.

### Values

**Name** | **Required** | **Description**
---------|--------------|----------------
**name** | Yes | Organization name.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Organization ID.
**name** | Organization name.
**slug** | A human-readable unique identifier, used for storing Organization data.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization



## PATCH Update an Organization

```shell
PATCH https://api.stackpoint.io/orgs/{Org ID}
```

> Example Request: Update the Organization name from the contents of a JSON file:

```shell
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-d @postorg.json \
"https://api.stackpoint.io/orgs/3"
```
> Contents of `postorg.json`:

```json
{
  "name": "New Organization Name"
}
```

> Alternate example: Update the Organization name as form data:

```shell
curl -X PATCH \
-H "Content-Type: multipart/form-data" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-F name="New Organization Name" \
"https://api.stackpoint.io/orgs/2"
```

> Example Response

```json
{
  "pk": 2,
  "name": "New Organization Name",
  "slug": "new-organization-name",
  "logo": null,
  "created": "2019-01-31T20:32:01.041059Z",
  "updated": "2019-01-31T21:21:07.607210Z"
}
```

> Example request: Update the Organization logo as form data:

```shell
curl -X PATCH \
-H "Content-Type: multipart/form-data" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-F logo=@/path/to/file.jpg \
"https://api.stackpoint.io/orgs/2"
```

> Example response:

```json
{
  "pk": 2,
  "name": "New Organization Name",
  "slug": "new-organization-name",
  "logo": "https:\/\/stackpoint_production.s3.amazonaws.com\/organization_logos\/logo.jpg",
  "created": "2016-08-05T14:35:53.161852Z",
  "updated": "2019-02-07T16:25:37.224597Z"
}
```

Update information for an existing Organization.

**Path Parameter**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.

### Values

**Name** | **Required** | **Description**
---------|--------------|----------------
**name** | Yes | Organization name.
**logo** | No | Organization logo. This value is `null` if a custom logo has not been set. To set a custom logo, send it as content type `multipart/form-data` as shown on the right.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Organization ID.
**name** | Organization name.
**slug** | A human-readable unique identifier, used for storing Organization data.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization
