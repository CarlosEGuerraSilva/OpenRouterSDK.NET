# Chat

## Overview

### Available Operations

* [Send](#send) - Create a chat completion

## Send

Sends a request for a model response for the given chat conversation. Supports both streaming and non-streaming modes.

### Example Usage

<!-- UsageSnippet language="csharp" operationID="sendChatCompletionRequest" method="post" path="/chat/completions" -->
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

var res = await sdk.Chat.SendAsync(chatGenerationParams: new ChatGenerationParams() {
    Messages = new List<Message>() {
        Message.CreateSystem(
            new SystemMessage() {
                Role = SystemMessageRole.System,
                Content = SystemMessageContent.CreateStr(
                    "You are a helpful assistant."
                ),
            }
        ),
        Message.CreateUser(
            new UserMessage() {
                Role = UserMessageRole.User,
                Content = UserMessageContent.CreateStr(
                    "What is the capital of France?"
                ),
            }
        ),
    },
    Temperature = 0.7D,
});

// Handle event stream response
if (res.Object != null)
{
    using (var eventStream = res.Object)
    {
        SendChatCompletionRequestResponseBody? eventData;
        while ((eventData = await eventStream.Next()) != null)
        {
            // handle eventData
        }
    }
}
// Handle JSON response
else if (res.ChatResponse != null)
{
    // handle JSON response
    var jsonResponse = res.ChatResponse;
}
```

### Parameters

| Parameter                                                                                                                                                                                                            | Type                                                                                                                                                                                                                 | Required                                                                                                                                                                                                             | Description                                                                                                                                                                                                          | Example                                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ChatGenerationParams`                                                                                                                                                                                               | [ChatGenerationParams](../../Models/Components/ChatGenerationParams.md)                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                   | N/A                                                                                                                                                                                                                  | {<br/>"messages": [<br/>{<br/>"role": "system",<br/>"content": "You are a helpful assistant."<br/>},<br/>{<br/>"role": "user",<br/>"content": "What is the capital of France?"<br/>}<br/>],<br/>"model": "openai/gpt-4",<br/>"temperature": 0.7,<br/>"max_tokens": 150<br/>} |
| `HTTPReferer`                                                                                                                                                                                                        | *string*                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                   | The app identifier should be your app's URL and is used as the primary identifier for rankings.<br/>This is used to track API usage per application.<br/>                                                            |                                                                                                                                                                                                                      |
| `XTitle`                                                                                                                                                                                                             | *string*                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                   | The app display name allows you to customize how your app appears in OpenRouter's dashboard.<br/>                                                                                                                    |                                                                                                                                                                                                                      |

### Response

**[SendChatCompletionRequestResponse](../../Models/Requests/SendChatCompletionRequestResponse.md)**

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