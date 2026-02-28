# Guardrails

## Overview

Guardrails endpoints

### Available Operations

* [List](#list) - List guardrails
* [Create](#create) - Create a guardrail
* [Get](#get) - Get a guardrail
* [Update](#update) - Update a guardrail
* [Delete](#delete) - Delete a guardrail
* [ListKeyAssignments](#listkeyassignments) - List all key assignments
* [ListMemberAssignments](#listmemberassignments) - List all member assignments
* [ListGuardrailKeyAssignments](#listguardrailkeyassignments) - List key assignments for a guardrail
* [BulkAssignKeys](#bulkassignkeys) - Bulk assign keys to a guardrail
* [ListGuardrailMemberAssignments](#listguardrailmemberassignments) - List member assignments for a guardrail
* [BulkAssignMembers](#bulkassignmembers) - Bulk assign members to a guardrail
* [BulkUnassignKeys](#bulkunassignkeys) - Bulk unassign keys from a guardrail
* [BulkUnassignMembers](#bulkunassignmembers) - Bulk unassign members from a guardrail

## List

List all guardrails for the authenticated user. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listGuardrails" method="get" path="/guardrails" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.ListAsync(
    offset: "0",
    limit: "50"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |
| `Offset`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Number of records to skip for pagination                                                                                                          | 0                                                                                                                                                 |
| `Limit`                                                                                                                                           | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Maximum number of records to return (max 100)                                                                                                     | 50                                                                                                                                                |

### Response

**[ListGuardrailsResponse](../../Models/Requests/ListGuardrailsResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## Create

Create a new guardrail for the authenticated user. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="createGuardrail" method="post" path="/guardrails" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.CreateAsync(requestBody: new CreateGuardrailRequestBody() {
    Name = "My New Guardrail",
});

// handle response
```

### Parameters

| Parameter                                                                                                                                                                                                                                   | Type                                                                                                                                                                                                                                        | Required                                                                                                                                                                                                                                    | Description                                                                                                                                                                                                                                 | Example                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RequestBody`                                                                                                                                                                                                                               | [CreateGuardrailRequestBody](../../Models/Requests/CreateGuardrailRequestBody.md)                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                          | N/A                                                                                                                                                                                                                                         | {<br/>"name": "My New Guardrail",<br/>"description": "A guardrail for limiting API usage",<br/>"limit_usd": 50,<br/>"reset_interval": "monthly",<br/>"allowed_providers": [<br/>"openai",<br/>"anthropic",<br/>"deepseek"<br/>],<br/>"allowed_models": null,<br/>"enforce_zdr": false<br/>} |
| `HTTPReferer`                                                                                                                                                                                                                               | *string*                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                          | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/>                                                                                   |                                                                                                                                                                                                                                             |
| `XTitle`                                                                                                                                                                                                                                    | *string*                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                          | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                                                                                                           |                                                                                                                                                                                                                                             |

### Response

**[CreateGuardrailResponse](../../Models/Requests/CreateGuardrailResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## Get

Get a single guardrail by ID. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getGuardrail" method="get" path="/guardrails/{id}" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.GetAsync(id: "550e8400-e29b-41d4-a716-446655440000");

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Id`                                                                                                                                              | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The unique identifier of the guardrail to retrieve                                                                                                | 550e8400-e29b-41d4-a716-446655440000                                                                                                              |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[GetGuardrailResponse](../../Models/Requests/GetGuardrailResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## Update

Update an existing guardrail. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="updateGuardrail" method="patch" path="/guardrails/{id}" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.UpdateAsync(
    id: "550e8400-e29b-41d4-a716-446655440000",
    requestBody: new UpdateGuardrailRequestBody() {}
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Id`                                                                                                                                              | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The unique identifier of the guardrail to update                                                                                                  | 550e8400-e29b-41d4-a716-446655440000                                                                                                              |
| `RequestBody`                                                                                                                                     | [UpdateGuardrailRequestBody](../../Models/Requests/UpdateGuardrailRequestBody.md)                                                                 | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               | {<br/>"name": "Updated Guardrail Name",<br/>"description": "Updated description",<br/>"limit_usd": 75,<br/>"reset_interval": "weekly"<br/>}       |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[UpdateGuardrailResponse](../../Models/Requests/UpdateGuardrailResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## Delete

Delete an existing guardrail. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="deleteGuardrail" method="delete" path="/guardrails/{id}" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.DeleteAsync(id: "550e8400-e29b-41d4-a716-446655440000");

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Id`                                                                                                                                              | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The unique identifier of the guardrail to delete                                                                                                  | 550e8400-e29b-41d4-a716-446655440000                                                                                                              |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[DeleteGuardrailResponse](../../Models/Requests/DeleteGuardrailResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## ListKeyAssignments

List all API key guardrail assignments for the authenticated user. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listKeyAssignments" method="get" path="/guardrails/assignments/keys" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.ListKeyAssignmentsAsync(
    offset: "0",
    limit: "50"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |
| `Offset`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Number of records to skip for pagination                                                                                                          | 0                                                                                                                                                 |
| `Limit`                                                                                                                                           | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Maximum number of records to return (max 100)                                                                                                     | 50                                                                                                                                                |

### Response

**[ListKeyAssignmentsResponse](../../Models/Requests/ListKeyAssignmentsResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## ListMemberAssignments

List all organization member guardrail assignments for the authenticated user. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listMemberAssignments" method="get" path="/guardrails/assignments/members" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.ListMemberAssignmentsAsync(
    offset: "0",
    limit: "50"
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |
| `Offset`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Number of records to skip for pagination                                                                                                          | 0                                                                                                                                                 |
| `Limit`                                                                                                                                           | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Maximum number of records to return (max 100)                                                                                                     | 50                                                                                                                                                |

### Response

**[ListMemberAssignmentsResponse](../../Models/Requests/ListMemberAssignmentsResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## ListGuardrailKeyAssignments

List all API key assignments for a specific guardrail. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listGuardrailKeyAssignments" method="get" path="/guardrails/{id}/assignments/keys" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

ListGuardrailKeyAssignmentsRequest req = new ListGuardrailKeyAssignmentsRequest() {
    Id = "550e8400-e29b-41d4-a716-446655440000",
    Offset = "0",
    Limit = "50",
};

var res = await sdk.Guardrails.ListGuardrailKeyAssignmentsAsync(req);

// handle response
```

### Parameters

| Parameter                                                                                         | Type                                                                                              | Required                                                                                          | Description                                                                                       |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `request`                                                                                         | [ListGuardrailKeyAssignmentsRequest](../../Models/Requests/ListGuardrailKeyAssignmentsRequest.md) | :heavy_check_mark:                                                                                | The request object to use for the request.                                                        |

### Response

**[ListGuardrailKeyAssignmentsResponse](../../Models/Requests/ListGuardrailKeyAssignmentsResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## BulkAssignKeys

Assign multiple API keys to a specific guardrail. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="bulkAssignKeysToGuardrail" method="post" path="/guardrails/{id}/assignments/keys" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;
using System.Collections.Generic;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.BulkAssignKeysAsync(
    id: "550e8400-e29b-41d4-a716-446655440000",
    requestBody: new BulkAssignKeysToGuardrailRequestBody() {
        KeyHashes = new List<string>() {
            "c56454edb818d6b14bc0d61c46025f1450b0f4012d12304ab40aacb519fcbc93",
        },
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Id`                                                                                                                                              | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The unique identifier of the guardrail                                                                                                            | 550e8400-e29b-41d4-a716-446655440000                                                                                                              |
| `RequestBody`                                                                                                                                     | [BulkAssignKeysToGuardrailRequestBody](../../Models/Requests/BulkAssignKeysToGuardrailRequestBody.md)                                             | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               |                                                                                                                                                   |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[BulkAssignKeysToGuardrailResponse](../../Models/Requests/BulkAssignKeysToGuardrailResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## ListGuardrailMemberAssignments

List all organization member assignments for a specific guardrail. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listGuardrailMemberAssignments" method="get" path="/guardrails/{id}/assignments/members" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

ListGuardrailMemberAssignmentsRequest req = new ListGuardrailMemberAssignmentsRequest() {
    Id = "550e8400-e29b-41d4-a716-446655440000",
    Offset = "0",
    Limit = "50",
};

var res = await sdk.Guardrails.ListGuardrailMemberAssignmentsAsync(req);

// handle response
```

### Parameters

| Parameter                                                                                               | Type                                                                                                    | Required                                                                                                | Description                                                                                             |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `request`                                                                                               | [ListGuardrailMemberAssignmentsRequest](../../Models/Requests/ListGuardrailMemberAssignmentsRequest.md) | :heavy_check_mark:                                                                                      | The request object to use for the request.                                                              |

### Response

**[ListGuardrailMemberAssignmentsResponse](../../Models/Requests/ListGuardrailMemberAssignmentsResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## BulkAssignMembers

Assign multiple organization members to a specific guardrail. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="bulkAssignMembersToGuardrail" method="post" path="/guardrails/{id}/assignments/members" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;
using System.Collections.Generic;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.BulkAssignMembersAsync(
    id: "550e8400-e29b-41d4-a716-446655440000",
    requestBody: new BulkAssignMembersToGuardrailRequestBody() {
        MemberUserIds = new List<string>() {
            "user_abc123",
            "user_def456",
        },
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Id`                                                                                                                                              | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The unique identifier of the guardrail                                                                                                            | 550e8400-e29b-41d4-a716-446655440000                                                                                                              |
| `RequestBody`                                                                                                                                     | [BulkAssignMembersToGuardrailRequestBody](../../Models/Requests/BulkAssignMembersToGuardrailRequestBody.md)                                       | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               |                                                                                                                                                   |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[BulkAssignMembersToGuardrailResponse](../../Models/Requests/BulkAssignMembersToGuardrailResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## BulkUnassignKeys

Unassign multiple API keys from a specific guardrail. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="bulkUnassignKeysFromGuardrail" method="post" path="/guardrails/{id}/assignments/keys/remove" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;
using System.Collections.Generic;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.BulkUnassignKeysAsync(
    id: "550e8400-e29b-41d4-a716-446655440000",
    requestBody: new BulkUnassignKeysFromGuardrailRequestBody() {
        KeyHashes = new List<string>() {
            "c56454edb818d6b14bc0d61c46025f1450b0f4012d12304ab40aacb519fcbc93",
        },
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Id`                                                                                                                                              | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The unique identifier of the guardrail                                                                                                            | 550e8400-e29b-41d4-a716-446655440000                                                                                                              |
| `RequestBody`                                                                                                                                     | [BulkUnassignKeysFromGuardrailRequestBody](../../Models/Requests/BulkUnassignKeysFromGuardrailRequestBody.md)                                     | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               |                                                                                                                                                   |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[BulkUnassignKeysFromGuardrailResponse](../../Models/Requests/BulkUnassignKeysFromGuardrailResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## BulkUnassignMembers

Unassign multiple organization members from a specific guardrail. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="bulkUnassignMembersFromGuardrail" method="post" path="/guardrails/{id}/assignments/members/remove" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;
using System.Collections.Generic;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Guardrails.BulkUnassignMembersAsync(
    id: "550e8400-e29b-41d4-a716-446655440000",
    requestBody: new BulkUnassignMembersFromGuardrailRequestBody() {
        MemberUserIds = new List<string>() {
            "user_abc123",
            "user_def456",
        },
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Id`                                                                                                                                              | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | The unique identifier of the guardrail                                                                                                            | 550e8400-e29b-41d4-a716-446655440000                                                                                                              |
| `RequestBody`                                                                                                                                     | [BulkUnassignMembersFromGuardrailRequestBody](../../Models/Requests/BulkUnassignMembersFromGuardrailRequestBody.md)                               | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               |                                                                                                                                                   |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[BulkUnassignMembersFromGuardrailResponse](../../Models/Requests/BulkUnassignMembersFromGuardrailResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |