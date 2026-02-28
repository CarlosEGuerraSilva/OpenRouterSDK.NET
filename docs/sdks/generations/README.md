# Generations

## Overview

Generation history endpoints

### Available Operations

* [GetGeneration](#getgeneration) - Get request & usage metadata for a generation

## GetGeneration

Get request & usage metadata for a generation

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getGeneration" method="get" path="/generation" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Generations.GetGenerationAsync(id: "<id>");

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Id`                                                                                                                                              | *string*                                                                                                                                          | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |

### Response

**[GetGenerationResponse](../../Models/Requests/GetGenerationResponse.md)**

### Errors

| Error Type                                                      | Status Code                                                     | Content Type                                                    |
| --------------------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException       | 401                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.PaymentRequiredResponseException    | 402                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.NotFoundResponseException           | 404                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException    | 429                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.InternalServerResponseException     | 500                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.BadGatewayResponseException         | 502                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.EdgeNetworkTimeoutResponseException | 524                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.ProviderOverloadedResponseException | 529                                                             | application/json                                                |
| OpenRouterSDK.Models.Errors.APIException                        | 4XX, 5XX                                                        | \*/\*                                                           |