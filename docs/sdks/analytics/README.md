# Analytics

## Overview

Analytics and usage endpoints

### Available Operations

* [GetUserActivity](#getuseractivity) - Get user activity grouped by endpoint

## GetUserActivity

Returns user activity data grouped by endpoint for the last 30 (completed) UTC days. [Management key](/docs/guides/overview/auth/management-api-keys) required.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="getUserActivity" method="get" path="/activity" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Analytics.GetUserActivityAsync(date: "2025-08-24");

// handle response
```

### Parameters

| Parameter                                                                                                                                         | Type                                                                                                                                              | Required                                                                                                                                          | Description                                                                                                                                       | Example                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HTTPReferer`                                                                                                                                     | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/> |                                                                                                                                                   |
| `XTitle`                                                                                                                                          | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                 |                                                                                                                                                   |
| `Date`                                                                                                                                            | *string*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                | Filter by a single UTC date in the last 30 days (YYYY-MM-DD format).                                                                              | 2025-08-24                                                                                                                                        |

### Response

**[GetUserActivityResponse](../../Models/Requests/GetUserActivityResponse.md)**

### Errors

| Error Type                                                  | Status Code                                                 | Content Type                                                |
| ----------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException     | 400                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException   | 401                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.ForbiddenResponseException      | 403                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.InternalServerResponseException | 500                                                         | application/json                                            |
| OpenRouterSDK.Models.Errors.APIException                    | 4XX, 5XX                                                    | \*/\*                                                       |