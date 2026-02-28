# Embeddings

## Overview

Text embedding endpoints

### Available Operations

* [Generate](#generate) - Submit an embedding request
* [ListModels](#listmodels) - List all embeddings models

## Generate

Submits an embedding request to the embeddings router

### Example Usage

<!-- UsageSnippet language="csharp" operationID="createEmbeddings" method="post" path="/embeddings" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Embeddings.GenerateAsync(requestBody: new CreateEmbeddingsRequestBody() {
    Input = InputUnion.CreateStr(
        "<value>"
    ),
    Model = "Taurus",
});

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RequestBody`                                                                                                                                     | [CreateEmbeddingsRequestBody](../../Models/Requests/CreateEmbeddingsRequestBody.md)                                                               | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |

### Response

**[CreateEmbeddingsResponse](../../Models/Requests/CreateEmbeddingsResponse.md)**

### Errors

| Error Type                                                      | Status Code                                                     | Content Type                                                    |
| --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException         | 400                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException       | 401                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.PaymentRequiredResponseException    | 402                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.NotFoundResponseException           | 404                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException    | 429                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.InternalServerResponseException     | 500                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.BadGatewayResponseException         | 502                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.ServiceUnavailableResponseException | 503                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.EdgeNetworkTimeoutResponseException | 524                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.ProviderOverloadedResponseException | 529                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.APIException                        | 4XX, 5XX                                                        | \*/\*                                                           |

## ListModels

Returns a list of all available embeddings models and their properties

### Example Usage

<!-- UsageSnippet language="csharp" operationID="listEmbeddingsModels" method="get" path="/embeddings/models" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Embeddings.ListModelsAsync();

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |

### Response

**[ListEmbeddingsModelsResponse](../../Models/Requests/ListEmbeddingsModelsResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |