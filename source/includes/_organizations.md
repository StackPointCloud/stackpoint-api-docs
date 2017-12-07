# Organizations

Organizations represent the highest level resource under which most of the infrastructure assets live.

When you log into Stackpoint.io for the first time, we automatically create an organization for you. You can customize the name and logo of this organization on the [Organization Setup](https://stackpoint.io/organization/setup) page.

## Get All Organizations

```shell
curl "https://api.stackpoint.io/orgs"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
[
  {
    "pk": 1,
    "name": "Hushy Wind",
    "slug": "hushy-wind",
    "logo": "https://stackpoint_production.s3.amazonaws.com/organization_logos/hushy_wind.jpg",
    "created": "2017-04-10T10:48:21.368163Z",
    "updated": "2017-04-10T10:48:21.368190Z"
  },
  {
    "pk": 2,
    "name": "Withered Spoon",
    "slug": "withered-spoon",
    "logo": "https://stackpoint_production.s3.amazonaws.com/organization_logos/withered_spoon.jpg",
    "created": "2016-05-24T23:30:45.866581Z",
    "updated": "2017-04-12T20:42:55.167792Z"
  }
]
```

This endpoint retrieves all organizations that you are associated with.

The `pk` attribute in the response denotes the organization ID.

### HTTP Request

`GET https://api.stackpoint.io/orgs`

## Get a Specific Organization

```shell
curl "https://api.stackpoint.io/orgs/1"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> The above command returns JSON structured like this:

```json
{
  "pk": 1,
  "name": "Hushy Wind",
  "slug": "hushy-wind",
  "logo": "https://stackpoint_production.s3.amazonaws.com/organization_logos/hushy_wind.jpg",
  "created": "2017-04-10T10:48:21.368163Z",
  "updated": "2017-04-10T10:48:21.368190Z"
}
```

This endpoint retrieves a specific organization.

### HTTP Request

`GET https://api.stackpoint.io/orgs/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | ID of the organization
