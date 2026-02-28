# Credits

## Overview

Credit management endpoints

### Available Operations

* [GetCredits](#getcredits) - Get remaining credits
* [CreateCoinbaseCharge](#createcoinbasecharge) - Create a Coinbase charge for crypto payment

## GetCredits

Get total credits purchased and used for the authenticated user. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getCredits" method="get" path="/credits" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Credits.GetCreditsAsync();

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |

### Response

**[GetCreditsResponse](../../Models/Requests/GetCreditsResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.ForbiddenResponseException      | 403                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## CreateCoinbaseCharge

Create a Coinbase charge for crypto payment

### Example Usage

<!-- UsageSnippet language="csharp" operationID="createCoinbaseCharge" method="post" path="/credits/coinbase" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>"
);

var res = await sdk.Credits.CreateCoinbaseChargeAsync(
    security: new CreateCoinbaseChargeSecurity() {
        Bearer = "<YOUR_BEARER_TOKEN_HERE>",
    },
    createChargeRequest: new CreateChargeRequest() {
        Amount = 100D,
        Sender = "0x1234567890123456789012345678901234567890",
        ChainId = ChainId.One,
    }
);

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `security`                                                                                                                                        | [CreateCoinbaseChargeSecurity](../../Models/Requests/CreateCoinbaseChargeSecurity.md)                                                             | :heavy_check_mark:                                                                                                                                | The security requirements to use for the request.                                                                                                 |                                                                                                                                                   |
| `CreateChargeRequest`                                                                                                                             | [CreateChargeRequest](../../Models/Components/CreateChargeRequest.md)                                                                             | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               | {<br/>"amount": 100,<br/>"sender": "0x1234567890123456789012345678901234567890",<br/>"chain_id": 1<br/>}                                          |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[CreateCoinbaseChargeResponse](../../Models/Requests/CreateCoinbaseChargeResponse.md)**

### Errors

| Error Type                                                   | Status Code                                                  | Content Type                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| OpenRouterSDK.Models.Errors.BadRequestResponseException      | 400                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException    | 401                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException | 429                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.InternalServerResponseException  | 500                                                          | application/json                                             |
| OpenRouterSDK.Models.Errors.APIException                     | 4XX, 5XX                                                     | \*/\*                                                        |