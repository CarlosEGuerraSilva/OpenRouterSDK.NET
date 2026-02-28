# Beta.Responses

## Overview

beta.responses endpoints

### Available Operations

* [Send](#send) - Create a response

## Send

Creates a streaming or non-streaming response using OpenResponses API format

### Example Usage

<!-- UsageSnippet language="csharp" operationID="createResponses" method="post" path="/responses" -->
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

var res = await sdk.Beta.Responses.SendAsync(openResponsesRequest: new OpenResponsesRequest() {});

// Handle event stream response
if (res.Object != null)
{
    using (var eventStream = res.Object)
    {
        CreateResponsesResponseBody? eventData;
        while ((eventData = await eventStream.Next()) != null)
        {
            // handle eventData
        }
    }
}
// Handle JSON response
else if (res.OpenResponsesNonStreamingResponse != null)
{
    // handle JSON response
    var jsonResponse = res.OpenResponsesNonStreamingResponse;
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                                                             | Type                                                                                                                                                                                                                                                                                                                                                                                                  | Required                                                                                                                                                                                                                                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                                                                                                                                           | Example                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `OpenResponsesRequest`                                                                                                                                                                                                                                                                                                                                                                                | [OpenResponsesRequest](../../Models/Components/OpenResponsesRequest.md)                                                                                                                                                                                                                                                                                                                               | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                                    | N/A                                                                                                                                                                                                                                                                                                                                                                                                   | {<br/>"model": "anthropic/claude-4.5-sonnet-20250929",<br/>"input": [<br/>{<br/>"type": "message",<br/>"content": "Hello, how are you?",<br/>"role": "user"<br/>}<br/>],<br/>"temperature": 0.7,<br/>"top_p": 0.9,<br/>"tools": [<br/>{<br/>"type": "function",<br/>"name": "get_current_weather",<br/>"description": "Get the current weather in a given location",<br/>"parameters": {<br/>"type": "object",<br/>"properties": {<br/>"location": {<br/>"type": "string"<br/>}<br/>}<br/>}<br/>}<br/>]<br/>} |
| `HTTPReferer`                                                                                                                                                                                                                                                                                                                                                                                         | *string*                                                                                                                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                    | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/>                                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                       |
| `XTitle`                                                                                                                                                                                                                                                                                                                                                                                              | *string*                                                                                                                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                    | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                       |

### Response

**[CreateResponsesResponse](../../Models/Requests/CreateResponsesResponse.md)**

### Errors

| Error Type                                                       | Status Code                                                      | Content Type                                                     |
| ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| OpenRouterSDK.Models.Errors.BadRequestResponseException          | 400                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.UnauthorizedResponseException        | 401                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.PaymentRequiredResponseException     | 402                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.NotFoundResponseException            | 404                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.RequestTimeoutResponseException      | 408                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.PayloadTooLargeResponseException     | 413                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.UnprocessableEntityResponseException | 422                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.TooManyRequestsResponseException     | 429                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.InternalServerResponseException      | 500                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.BadGatewayResponseException          | 502                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.ServiceUnavailableResponseException  | 503                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.EdgeNetworkTimeoutResponseException  | 524                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.ProviderOverloadedResponseException  | 529                                                              | application/json                                                 |
| OpenRouterSDK.Models.Errors.APIException                         | 4XX, 5XX                                                         | \*/\*                                                            |