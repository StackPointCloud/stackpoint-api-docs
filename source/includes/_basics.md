# Getting Started

Welcome to the NetApp Kubernetes Service (NKS) API Reference. This section guides you through the setup process of creating an NKS API token, passing the token in your API requests, and the response codes returned by the API.

## Resource URL

The full resource URL for the NKS API is `https://api.stackpoint.io`.

## Authorization Requirements

All API requests must be authenticated with your API token. To obtain a token:

1. Register or log in at https://nks.netapp.io.
2. Click your profile avatar in the top right corner and select `Edit Profile`.
3. In the **API Tokens** section, click **Add Token**.
4. Copy the token and save it somewhere safe. This is your only chance to view your API token. The token cannot be displayed after you leave or reload the page.

NOTE: The API only accepts keys from accounts which have the role of `Owner` in the related Organization.

## Usage

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdev123456789" \
"https://api.stackpoint.io/orgs"
```

To authenticate, you must pass the API token as a Bearer token in the Authorization header for all API requests.

To do this, add `-H "Authorization: Bearer {your API token}"` to the request, as demonstrated in the example on the right.

### Organization Number

After you create an API token, the page displays the example code to use it. This code includes your current organization ID, which is a critical component in your future API requests.

Note: You can also fetch your current organization ID from [the Organizations resource](#organizations).

In this example, the user's organization ID is `381`:

![API token example code](/source/images/api-token-example-code.png?raw=true "API token example code")


### Example

```shell
curl -X GET \
-H "Authorization: Bearer {API token}" \
"https://api.stackpoint.io/orgs/{Org ID}/clusters"
```

The query on the right returns a list of your current active clusters within the selected organization.

> For example:

```shell
curl -X GET \
-H "Authorization: Bearer abcdef123456789abcdev123456789" \
"https://api.stackpoint.io/orgs/381/clusters"
```

## Response Codes

> Example using the `-i` flag to view all headers:

```shell
curl -i -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer abcdef123456789abcdev123456789" \
-d @updateorg.json "https://api.stackpoint.io/orgs/381"
```

> This query will trigger a 400 error. Using the -i flag returns the additional response:

```json
{"detail":"JSON parse error - Expecting property name enclosed in double quotes: line 1 column 72 (char 71)"}
```

The NKS API uses the following response codes:

Response | Description
---------|------------
**200** | OK: The request succeeded.
**400** | Bad Request: The data sent with the request is not valid. For more details, use the `-i` flag in your request to view all headers. This returns additional information about the cause of the error.
**401** | Unauthorized: "Authentication credentials were not provided." You did not provide an API key, or the provided API key is invalid.
**403** | Forbidden: You are not allowed to access this endpoint or resource.
**404** | Not Found: The endpoint or resource was not found.
**405** | Method Not Allowed: The endpoint does not allow this method.
**500** | Internal Server Error: We had a problem with our server. Try again later.
**503** | Service Unavailable: We are temporarily offline or experiencing an outage. If this error persists, please contact our support department.
