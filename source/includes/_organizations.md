# Organizations

## Overview

Organizations are the highest-level resource. The Organizations resource contains information about the Organization. This includes the ID, which is required for most other API calls.

### Background

The first time you log in to Stackpoint.io, we automatically create an Organization for you. You can customize the name and logo of this Organization on the [Organization Setup](https://stackpoint.io/organization/setup) page.

## GET /orgs

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
    "pk": 11644,
    "name": "Company Organization",
    "slug": "company-organization",
    "logo": null,
    "created": "2018-09-24T18:23:22.889260Z",
    "updated": "2018-09-24T18:23:22.889291Z"
  },
  {
    "pk": 381,
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

## POST /orgs

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
  "name": "My New Organization",
}
```

>  Example Response. If the new Organization is created successfully, the API will return a list of all Organizations of which the user is a member, including the newly-created Organization. The new Organization is listed first.

```json
[
 {
    "pk": 15055,
    "name": "My New Organization",
    "slug": "my-new-organization",
    "logo": null,
    "created": "2019-01-31T20:32:01.041059Z",
    "updated": "2019-01-31T20:32:01.041093Z"
},
  {
    "pk": 381,
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
**logo** | Organization logo. This value is `null` if a custom logo has not been set. To set a custom logo, send the request as content type `application/x-www-form-urlencoded`.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Organization ID.
**name** | Organization name.
**slug** | A human-readable unique identifier, used for storing Organization data.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization

## GET /orgs/{Org ID}

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/381"
```

> Example response:

```json
{
  "pk": 381,
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

## PATCH /orgs/{Org ID}

> Example Request

```shell
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-d @postorg.json \
"https://api.stackpoint.io/orgs/{Org_ID}"
```
> Contents of `postorg.json`:

```json
{
  "name": "New Organization Name",
  "slug": "new-organization-name"
}
```

> Example Response

```json
{
  "pk": 15055,
  "name": "New Organization Name",
  "slug": "new-organization-name",
  "logo": null,
  "created": "2019-01-31T20:32:01.041059Z",
  "updated": "2019-01-31T21:21:07.607210Z"
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
**logo** | Organization logo. This value is `null` if a custom logo has not been set. To set a custom logo, send the request as content type `application/x-www-form-urlencoded`.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Organization ID.
**name** | Organization name.
**slug** | A human-readable unique identifier, used for storing Organization data.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization
