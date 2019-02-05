# Organizations

## Overview

Organizations are the highest-level resource. The Organizations resource contains information about the Organization. This includes the ID, which is required for most other API calls.

### Background

The first time you log in to Stackpoint.io, we automatically create an Organization for you. You can customize the name and logo of this Organization on the [Organization Setup](https://stackpoint.io/organization/setup) page.

## GET /orgs

> Example request:

```
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs"
```

> Example response:

```
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
**slug** | A human-readable unique identifier, used for storing Organization data. The only allowed characters are the 26 US ANSI letters (upper or lowercase), numbers, dashes, and hyphens. 50 characters max. Example: `my-organization`.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization

## POST /orgs

> Example Request:

```
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-d @postorg.json \
"https://api.stackpoint.io/orgs"
```

> Contents of `postorg.json`:

```
{
  "name": "My New Organization",
  "slug": "my-new-organization"
}
```

>  Example Response. If the new Organization is created successfully, the API will return a list of all Organizations of which the user is a member, including the newly-created Organization. The new Organization is listed first.

```
[
 {
    pk": 15055,
    "name": "My New Organization",
    "slug": "my-new-organization",
    "logo": "null",
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
**slug** | No | A human-readable unique identifier, used for storing Organization data. The only allowed characters are the 26 US ANSI letters (upper or lowercase), numbers, dashes, and hyphens. 50 characters max. Example: `my-organization`.
**logo** | No | URL of the Organization logo. This value is `null` if a custom logo has not been set.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Organization ID.
**name** | Organization name.
**slug** | A human-readable unique identifier, used for storing Organization data. The only allowed characters are the 26 US ANSI letters (upper or lowercase), numbers, dashes, and hyphens. 50 characters max. Example: `my-organization`.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization

## GET /orgs/{Org ID}

> Example request:

```
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/381"
```

> Example response:

```
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
**slug** | A human-readable unique identifier, used for storing Organization data. The only allowed characters are the 26 US ANSI letters (upper or lowercase), numbers, dashes, and hyphens. 50 characters max. Example: `my-organization`.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization

## PATCH /orgs/{Org ID}

> Example Request

```
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-d @postorg.json \
"https://api.stackpoint.io/orgs"
```
> Contents of `postorg.json`:

```
{
  "name": "New Organization Name",
  "slug": "new-organization-name"
}
```

> Example Response

```
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
**slug** | No | A human-readable unique identifier, used for storing Organization data. The only allowed characters are the 26 US ANSI letters (upper or lowercase), numbers, dashes, and hyphens. 50 characters max. Example: `my-organization`.
**logo** | No | URL of the Organization logo. This value is `null` if a custom logo has not been set.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Organization ID.
**name** | Organization name.
**slug** | A human-readable unique identifier, used for storing Organization data. The only allowed characters are the 26 US ANSI letters (upper or lowercase), numbers, dashes, and hyphens. 50 characters max. Example: `my-organization`.
**logo** | Organization logo. This value is `null` if a custom logo has not been set.
**created** | Timestamp of the Organization's create date.
**updated** | Timestamp of the last update to the Organization
