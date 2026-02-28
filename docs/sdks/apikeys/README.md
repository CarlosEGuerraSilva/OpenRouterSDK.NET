# APIKeys

## Overview

API key management endpoints

### Available Operations

* [List](#list) - List API keys
* [Create](#create) - Create a new API key
* [Update](#update) - Update an API key
* [Delete](#delete) - Delete an API key
* [Get](#get) - Get a single API key
* [GetCurrentKeyMetadata](#getcurrentkeymetadata) - Get current API key

## List

List all API keys for the authenticated user. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="list" method="get" path="/keys" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.APIKeys.ListAsync(
    includeDisabled: "false",
    offset: "0"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |
| `IncludeDisabled`                                                                                                                                 | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Whether to include disabled API keys in the response                                                                                              | false                                                                                                                                             |
| `Offset`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Number of API keys to skip for pagination                                                                                                         | 0                                                                                                                                                 |

### Response

**[ListResponse](../../Models/Requests/ListResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException    | 401                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException | 429                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.InternalServerResponseException  | 500                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.APIException                     | 4XX, 5XX                                                     | \*/\*                                                        |

## Create

Create a new API key for the authenticated user. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="createKeys" method="post" path="/keys" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.APIKeys.CreateAsync(requestBody: new CreateKeysRequestBody() {
    Name = "My New API Key",
});

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RequestBody`                                                                                                                                     | [CreateKeysRequestBody](../../Models/Requests/CreateKeysRequestBody.md)                                                                           | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               | {<br/>"name": "My New API Key",<br/>"limit": 50,<br/>"limit_reset": "monthly",<br/>"include_byok_in_limit": true,<br/>"expires_at": "2027-12-31T23:59:59Z"<br/>} |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[CreateKeysResponse](../../Models/Requests/CreateKeysResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| OpenRouterSDK.Models.Errors.BadRequestResponseException      | 400                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException    | 401                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException | 429                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.InternalServerResponseException  | 500                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.APIException                     | 4XX, 5XX                                                     | \*/\*                                                        |

## Update

Update an existing API key. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateKeys" method="patch" path="/keys/{hash}" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.APIKeys.UpdateAsync(
    hash: "f01d52606dc8f0a8303a7b5cc3fa07109c2e346cec7c0a16b40de462992ce943",
    requestBody: new UpdateKeysRequestBody() {}
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Hash`                                                                                                                                            | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The hash identifier of the API key to update                                                                                                      | f01d52606dc8f0a8303a7b5cc3fa07109c2e346cec7c0a16b40de462992ce943                                                                                  |
| `RequestBody`                                                                                                                                     | [UpdateKeysRequestBody](../../Models/Requests/UpdateKeysRequestBody.md)                                                                           | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               | {<br/>"name": "Updated API Key Name",<br/>"disabled": false,<br/>"limit": 75,<br/>"limit_reset": "daily",<br/>"include_byok_in_limit": true<br/>} |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[UpdateKeysResponse](../../Models/Requests/UpdateKeysResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| OpenRouterSDK.Models.Errors.BadRequestResponseException      | 400                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException    | 401                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.NotFoundResponseException        | 404                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException | 429                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.InternalServerResponseException  | 500                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.APIException                     | 4XX, 5XX                                                     | \*/\*                                                        |

## Delete

Delete an existing API key. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="deleteKeys" method="delete" path="/keys/{hash}" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.APIKeys.DeleteAsync(hash: "f01d52606dc8f0a8303a7b5cc3fa07109c2e346cec7c0a16b40de462992ce943");

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Hash`                                                                                                                                            | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The hash identifier of the API key to delete                                                                                                      | f01d52606dc8f0a8303a7b5cc3fa07109c2e346cec7c0a16b40de462992ce943                                                                                  |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[DeleteKeysResponse](../../Models/Requests/DeleteKeysResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException    | 401                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.NotFoundResponseException        | 404                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException | 429                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.InternalServerResponseException  | 500                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.APIException                     | 4XX, 5XX                                                     | \*/\*                                                        |

## Get

Get a single API key by hash. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getKey" method="get" path="/keys/{hash}" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.APIKeys.GetAsync(hash: "f01d52606dc8f0a8303a7b5cc3fa07109c2e346cec7c0a16b40de462992ce943");

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Hash`                                                                                                                                            | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The hash identifier of the API key to retrieve                                                                                                    | f01d52606dc8f0a8303a7b5cc3fa07109c2e346cec7c0a16b40de462992ce943                                                                                  |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[GetKeyResponse](../../Models/Requests/GetKeyResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException    | 401                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.NotFoundResponseException        | 404                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException | 429                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.InternalServerResponseException  | 500                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.APIException                     | 4XX, 5XX                                                     | \*/\*                                                        |

## GetCurrentKeyMetadata

Get information on the API key associated with the current authentication session

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getCurrentKey" method="get" path="/key" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.APIKeys.GetCurrentKeyMetadataAsync();

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |

### Response

**[GetCurrentKeyResponse](../../Models/Requests/GetCurrentKeyResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |