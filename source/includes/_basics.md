# Introduction

Welcome to the StackPointCloud API Reference. You can use our API to create Kubernetes clusters on AWS, Azure, DigitalOcean, GKE & GCE and install various cloud native applications.

The endpoints are described in this panel while examples can be found on the right panel.

# Authentication

> To authenticate with the StackPointCloud API, you will need to use an API token.

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.stackpoint.io/orgs"
  -H "Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5"
```

> Make sure to replace `d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5` with your API key.

StackPointCloud uses API keys to allow access to the API. To obatin a key:

1. Register or login at [Stackpoint.io](https://stackpoint.io)
2. Click you profile avatar on the top right corner of the page and select `Edit Profile` or visit [the profile page](https://stackpoint.io/user/profile) directly
3. Scroll down until you see the `API Tokens` section and click the `Add Token` button
4. Copy the token and save it somewhere safe, it won't be displayed anymore if you reload the page

The API key should be included in all API request to the server in a header that looks like the following:

`Authorization: Bearer d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5`

<aside class="notice">
You must replace <code>d0bf933f1a9f2c04f99e4bc713289fbb35abb3a5</code> with your personal API key.
</aside>

# Response Codes

Stackpoint API uses the following response codes:

Response Code | Meaning
------------- | -------
400 | Bad Request -- The data sent with the request is not valid
401 | Unauthorized -- You have not provided an API key or provided an invalid API key
403 | Forbidden -- You are not allowed to access this endpoint or resource
404 | Not Found -- The endpoint or resource was not found
405 | Method Not Allowed -- The endpoint does not allow this method
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline or experiencing outage. Please try again later.
