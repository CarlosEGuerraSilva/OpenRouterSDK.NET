# OAuth

## Overview

OAuth authentication endpoints

### Available Operations

* [ExchangeAuthCodeForAPIKey](#exchangeauthcodeforapikey) - Exchange authorization code for API key
* [CreateAuthCode](#createauthcode) - Create authorization code

## ExchangeAuthCodeForAPIKey

Exchange an authorization code from the PKCE flow for a user-controlled API key

### Example Usage

<!-- UsageSnippet language="csharp" operationID="exchangeAuthCodeForAPIKey" method="post" path="/auth/keys" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.OAuth.ExchangeAuthCodeForAPIKeyAsync(requestBody: new ExchangeAuthCodeForAPIKeyRequestBody() {
    Code = "auth_code_abc123def456",
});

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RequestBody`                                                                                                                                     | [ExchangeAuthCodeForAPIKeyRequestBody](../../Models/Requests/ExchangeAuthCodeForAPIKeyRequestBody.md)                                             | :heavy_check_mark:                                                                                                                                | N/A                                                                                                                                               | {<br/>"code": "auth_code_abc123def456",<br/>"code_verifier": "dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk",<br/>"code_challenge_method": "S256"<br/>} |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |

### Response

**[ExchangeAuthCodeForAPIKeyResponse](../../Models/Requests/ExchangeAuthCodeForAPIKeyResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.ForbiddenResponseException      | 403                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |

## CreateAuthCode

Create an authorization code for the PKCE flow to generate a user-controlled API key

### Example Usage

<!-- UsageSnippet language="csharp" operationID="createAuthKeysCode" method="post" path="/auth/keys/code" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.OAuth.CreateAuthCodeAsync(requestBody: new CreateAuthKeysCodeRequestBody() {
    CallbackUrl = "https://myapp.com/auth/callback",
});

// handle response
```

### Parameters

| Parameter                                                                                                                                                             | Type                                                                                                                                                                  | Required                                                                                                                                                              | Description                                                                                                                                                           | Example                                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `RequestBody`                                                                                                                                                         | [CreateAuthKeysCodeRequestBody](../../Models/Requests/CreateAuthKeysCodeRequestBody.md)                                                                               | :heavy_check_mark:                                                                                                                                                    | N/A                                                                                                                                                                   | {<br/>"callback_url": "https://myapp.com/auth/callback",<br/>"code_challenge": "E9Melhoa2OwvFrEMTJguCHaoeK1t8URWbuGJSstw-cM",<br/>"code_challenge_method": "S256",<br/>"limit": 100<br/>} |
| `HTTPReferer`                                                                                                                                                         | *string*                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                    | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/>             |                                                                                                                                                                       |
| `XTitle`                                                                                                                                                              | *string*                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                    | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                                     |                                                                                                                                                                       |

### Response

**[CreateAuthKeysCodeResponse](../../Models/Requests/CreateAuthKeysCodeResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |