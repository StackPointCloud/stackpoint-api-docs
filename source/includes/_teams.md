# Teams

## Overview

Teams allow you to organize your users into groups, in order to manage their access rights.

## GET All Teams

```shell
GET https://api.stackpoint.io/orgs/{Org ID}/teams
```

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/teams"
```
> Example response:

```json
[
  {
    "pk": 3,
    "name": "Everyone",
    "slug": "everyone",
    "org": 3,
    "is_org_wide": true,
    "created": "2019-02-12T20:11:53.481354Z",
    "memberships": [
      {
        "pk": 3,
        "user": {
          "pk": 3,
          "username": "jdoe",
          "email": "jdoe@example.com",
          "first_name": "",
          "last_name": "",
          "full_name": "",
          "date_joined": "2019-02-01T18:01:29.685916Z"
        },
        "team": 3,
        "created": "2019-02-12T20:11:53.570746Z"
      }
    ]
  }
]
```

Get the list of Teams for the specified Organization.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Team ID.
**name** | Team name.
**slug** | A human-readable unique identifier, used for storing Team data.
**org** | The Organization ID.
**is_org_wide** | Whether or not the Team is restricted to a particular Workspace.
**created** | The Team creation timestamp.
**memberships** | A list of users assigned to this Team.
**username** | The user's username.
**email** | The user's email address.
**first_name** | The user's first name.
**last_name** | The user's last name.
**full_name** | The user's full name.

## GET a Specific Team

```shell
GET https://api.stackpoint.io/orgs/{Org ID}/teams/{Team ID}
```

> Example request:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/teams/3"
```

> Example response:

```json
{
  "pk": 3,
  "name": "Everyone",
  "slug": "everyone",
  "org": 3,
  "is_org_wide": true,
  "created": "2019-02-12T20:11:53.481354Z",
  "memberships": [
    {
      "pk": 3,
      "user": {
        "pk": 3,
        "username": "jdoe",
        "email": "jdoe@example.com",
        "first_name": "",
        "last_name": "",
        "full_name": "",
        "date_joined": "2019-02-01T18:01:29.685916Z"
      },
      "team": 3,
      "created": "2019-02-12T20:11:53.570746Z"
    }
  ]
}
```

Get information for a specific Team.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Team ID** | Yes | The Team ID.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Team ID.
**name** | Team name.
**slug** | A human-readable unique identifier, used for storing Team data.
**org** | The Organization ID.
**is_org_wide** | Whether or not the Team is restricted to a particular Workspace.
**created** | The Team creation timestamp.
**memberships** | A list of users assigned to this Team.
**username** | The user's username.
**email** | The user's email address.
**first_name** | The user's first name.
**last_name** | The user's last name.
**full_name** | The user's full name.

## POST Create a New Team

```shell
POST https://api.stackpoint.io/orgs/{Org ID}/teams
```

> Example Request:

```shell
curl -X POST \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-d @add-team.json \
"https://api.stackpoint.io/orgs/3/teams"
```

> Contents of `add-team.json`:

```shell
{
  "name": "My New Team"
}
```

> Example response:

```json
{
  "pk": 4,
  "name": "My New Team",
  "slug": "my-new-team",
  "org": 3,
  "is_org_wide": false,
  "created": "2019-03-01T19:52:23.087626Z",
  "memberships": [

  ]
}
```

Create a new Team in the specified Organization.

### Values

**Name** | **Required** | **Type** | **Description**
---------|--------------|----------|---------------
**name** | Yes | String | Team name.
**is_org_wide** | No | Boolean | Whether or not the Team is restricted to a particular Workspace. Allowed values are `true` or `false`.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Team ID.
**name** | Team name.
**slug** | A human-readable unique identifier, used for storing Team data.
**org** | The Organization ID.
**is_org_wide** | Whether or not the Team is restricted to a particular Workspace.
**created** | The Team creation timestamp.

## PATCH Update a Team

```shell
PATCH https://api.stackpoint.io/orgs/{Org ID}/teams/{Team ID}
```

> Example Request: Add the first user to the team from the contents of a JSON file.
> NOTE: See warning about adding additional users.

```shell
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
-d @add-team-member.json \
"https://api.stackpoint.io/orgs/3/teams/3"
```
> Contents of `add-team-member.json`:

```json
{
  "memberships": [
    {
      "user": 3
    }
  ]
}
```

> Example response:

```json
{
  "pk": 3,
  "name": "Everyone",
  "slug": "everyone",
  "org": 3,
  "is_org_wide": true,
  "created": "2019-02-12T20:11:53.481354Z",
  "memberships": [
    {
      "pk": 4,
      "user": {
        "pk": 3,
        "username": "jdoe",
        "email": "jdoe@example.com",
        "first_name": "",
        "last_name": "",
        "full_name": "",
        "date_joined": "2019-02-01T18:01:29.685916Z"
      },
      "team": 3,
      "created": "2019-03-01T20:32:15.325914Z"
    }
  ]
}
```

Update the specified Team. This example adds the first user to the Team.

<aside class="warning">WARNING: You must include ALL users in your request, not just the new user. The contents of this file will overwrite the existing list of users on the Team.  </aside>

For example, to add a second user to the team, the contents of `add-team-member.json` should read:

`{"memberships":[{"user":3},{"user":4}]}`

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Team ID** | Yes | The Team ID.

### Values

**Name** | **Type** | **Description**
---------|----------|---------------
**name** | String | Team name.
**is_org_wide** | Boolean | Whether or not the Team is restricted to a particular Workspace. Allowed values are `true` or `false`.
**memberships** | Update the list of users.
**user** | The user ID.
**username** | The user name.
**email** | The user's email address.
**first_name** | The user's first name.
**last_name** | The user's last name.
**full_name** | The user's full name.

### Return Values

**Name** | **Description**
---------|-----------------
**pk** | Team ID.
**name** | Team name.
**slug** | A human-readable unique identifier, used for storing Team data.
**org** | The Organization ID.
**is_org_wide** | Whether or not the Team is restricted to a particular Workspace.
**created** | The Team creation timestamp.
**memberships** | Update the list of users.
**user** | The user ID.
**username** | The user name.
**email** | The user's email address.
**first_name** | The user's first name.
**last_name** | The user's last name.
**full_name** | The user's full name.

## DELETE a Team

```shell
DELETE https://api.stackpoint.io/orgs/{Org ID}/teams/{Team ID}
```

> Example request:

```shell
curl -X DELETE \
-H "Authorization: Bearer abcdef123456789abcdef123456789" \
"https://api.stackpoint.io/orgs/3/teams/3"
```

> If the team is successfully deleted, this command returns an empty response with status code `204`.

Delete the specified Team.

**Path Parameters**

**Name** | **Required** | **Description**
-----|----------|-------------
**Org ID** | Yes | The Organization ID.
**Team ID** | Yes | The Team ID.
