<!-- Start SDK Example Usage [usage] -->
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
<!-- End SDK Example Usage [usage] -->