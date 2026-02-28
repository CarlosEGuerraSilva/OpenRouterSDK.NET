# AIModels

## Overview

### Available Operations

* [Count](#count) - Get total count of available models
* [List](#list) - List all models and their properties
* [ListUser](#listuser) - List models filtered by user provider preferences, privacy settings, and guardrails

## Count

Get total count of available models

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listModelsCount" method="get" path="/models/count" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.AIModels.CountAsync();

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |

### Response

**[ListModelsCountResponse](../../Models/Requests/ListModelsCountResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## List

List all models and their properties

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getModels" method="get" path="/models" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.AIModels.ListAsync(category: Category.Programming);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |
| `Category`                                                                                                                                        | [Category](../../Models/Requests/Category.md)                                                                                                     | :heavy_minus_sign:                                                                                                                                | Filter models by use case category                                                                                                                | programming                                                                                                                                       |
| `SupportedParameters`                                                                                                                             | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | N/A                                                                                                                                               |                                                                                                                                                   |

### Response

**[GetModelsResponse](../../Models/Requests/GetModelsResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## ListUser

List models filtered by user provider preferences, [privacy settings](https://openrouter.ai/docs/guides/privacy/logging), and [guardrails](https://openrouter.ai/docs/guides/features/guardrails). If requesting through `eu.openrouter.ai/api/v1/...` the results will be filtered to models that satisfy [EU in-region routing](https://openrouter.ai/docs/guides/privacy/logging#enterprise-eu-in-region-routing).

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listModelsUser" method="get" path="/models/user" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>"
);

var res = await sdk.AIModels.ListUserAsync(security: new ListModelsUserSecurity() {
    Bearer = "<YOUR_BEARER_TOKEN_HERE>",
});

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                        | [ListModelsUserSecurity](../../Models/Requests/ListModelsUserSecurity.md)                                                                         | :heavy_check_mark:                                                                                                                                | The security requirements to use for the request.                                                                                                 |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |

### Response

**[ListModelsUserResponse](../../Models/Requests/ListModelsUserResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.NotFoundResponseException       | 404                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |