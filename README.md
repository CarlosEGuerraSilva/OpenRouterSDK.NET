# OpenRouterSDK

Developer-friendly & type-safe Csharp SDK specifically catered to leverage *OpenRouterSDK* API.

[![Built by Speakeasy](https://img.shields.io/badge/Built_by-SPEAKEASY-374151?style=for-the-badge&labelColor=f3f4f6)](https://www.speakeasy.com/?utm_source=open-router-sdk&utm_campaign=csharp)
[![License: MIT](https://img.shields.io/badge/LICENSE_//_MIT-3b5bdb?style=for-the-badge&labelColor=eff6ff)](https://opensource.org/licenses/MIT)


<br /><br />
> [!IMPORTANT]
> This SDK is not yet ready for production use. Still in active development, and there may be breaking changes without a major version update. We recommend pinning usage to a specific package version until the SDK reaches a stable release.

<!-- Start Summary [summary] -->
## Summary

OpenRouter API: OpenAI-compatible API with additional OpenRouter features

For more information about the API: [OpenRouter Documentation](https://openrouter.ai/docs)
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [OpenRouterSDK](#openroutersdk)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Server-sent event streaming](#server-sent-event-streaming)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Custom HTTP Client](#custom-http-client)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

To add a reference to a local instance of the SDK in a .NET project:
```bash
dotnet add reference src/OpenRouterSDK/OpenRouterSDK.csproj
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

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

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name     | Type | Scheme      |
| -------- | ---- | ----------- |
| `ApiKey` | http | HTTP Bearer |

To authenticate with the API the `ApiKey` parameter must be set when initializing the SDK client instance. For example:
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    apiKey: "<YOUR_BEARER_TOKEN_HERE>",
    httpReferer: "<value>",
    xTitle: "<value>"
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

### Per-Operation Security Schemes

Some operations in this SDK require the security scheme to be specified at the request level. For example:
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
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [AIModels](docs/sdks/aimodels/README.md)

* [Count](docs/sdks/aimodels/README.md#count) - Get total count of available models
* [List](docs/sdks/aimodels/README.md#list) - List all models and their properties
* [ListUser](docs/sdks/aimodels/README.md#listuser) - List models filtered by user provider preferences, privacy settings, and guardrails

### [Analytics](docs/sdks/analytics/README.md)

* [GetUserActivity](docs/sdks/analytics/README.md#getuseractivity) - Get user activity grouped by endpoint

### [APIKeys](docs/sdks/apikeys/README.md)

* [List](docs/sdks/apikeys/README.md#list) - List API keys
* [Create](docs/sdks/apikeys/README.md#create) - Create a new API key
* [Update](docs/sdks/apikeys/README.md#update) - Update an API key
* [Delete](docs/sdks/apikeys/README.md#delete) - Delete an API key
* [Get](docs/sdks/apikeys/README.md#get) - Get a single API key
* [GetCurrentKeyMetadata](docs/sdks/apikeys/README.md#getcurrentkeymetadata) - Get current API key

### [Beta.Responses](docs/sdks/responses/README.md)

* [Send](docs/sdks/responses/README.md#send) - Create a response

### [Chat](docs/sdks/chat/README.md)

* [Send](docs/sdks/chat/README.md#send) - Create a chat completion

### [Credits](docs/sdks/credits/README.md)

* [GetCredits](docs/sdks/credits/README.md#getcredits) - Get remaining credits
* [CreateCoinbaseCharge](docs/sdks/credits/README.md#createcoinbasecharge) - Create a Coinbase charge for crypto payment

### [Embeddings](docs/sdks/embeddings/README.md)

* [Generate](docs/sdks/embeddings/README.md#generate) - Submit an embedding request
* [ListModels](docs/sdks/embeddings/README.md#listmodels) - List all embeddings models

### [Endpoints](docs/sdks/endpoints/README.md)

* [List](docs/sdks/endpoints/README.md#list) - List all endpoints for a model
* [ListZdrEndpoints](docs/sdks/endpoints/README.md#listzdrendpoints) - Preview the impact of ZDR on the available endpoints

### [Generations](docs/sdks/generations/README.md)

* [GetGeneration](docs/sdks/generations/README.md#getgeneration) - Get request & usage metadata for a generation

### [Guardrails](docs/sdks/guardrails/README.md)

* [List](docs/sdks/guardrails/README.md#list) - List guardrails
* [Create](docs/sdks/guardrails/README.md#create) - Create a guardrail
* [Get](docs/sdks/guardrails/README.md#get) - Get a guardrail
* [Update](docs/sdks/guardrails/README.md#update) - Update a guardrail
* [Delete](docs/sdks/guardrails/README.md#delete) - Delete a guardrail
* [ListKeyAssignments](docs/sdks/guardrails/README.md#listkeyassignments) - List all key assignments
* [ListMemberAssignments](docs/sdks/guardrails/README.md#listmemberassignments) - List all member assignments
* [ListGuardrailKeyAssignments](docs/sdks/guardrails/README.md#listguardrailkeyassignments) - List key assignments for a guardrail
* [BulkAssignKeys](docs/sdks/guardrails/README.md#bulkassignkeys) - Bulk assign keys to a guardrail
* [ListGuardrailMemberAssignments](docs/sdks/guardrails/README.md#listguardrailmemberassignments) - List member assignments for a guardrail
* [BulkAssignMembers](docs/sdks/guardrails/README.md#bulkassignmembers) - Bulk assign members to a guardrail
* [BulkUnassignKeys](docs/sdks/guardrails/README.md#bulkunassignkeys) - Bulk unassign keys from a guardrail
* [BulkUnassignMembers](docs/sdks/guardrails/README.md#bulkunassignmembers) - Bulk unassign members from a guardrail

### [OAuth](docs/sdks/oauth/README.md)

* [ExchangeAuthCodeForAPIKey](docs/sdks/oauth/README.md#exchangeauthcodeforapikey) - Exchange authorization code for API key
* [CreateAuthCode](docs/sdks/oauth/README.md#createauthcode) - Create authorization code

### [Providers](docs/sdks/providers/README.md)

* [List](docs/sdks/providers/README.md#list) - List all providers

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Server-sent event streaming [eventstream] -->
## Server-sent event streaming

Server-sent events (SSE) are used to stream content from certain operations. SSE is a web standard that allows a server to push data to a client over a single HTTP connection in real-time.

These operations return an instance of `EventStream`, which implements `IDisposable`. It should be consumed using the RAII (Resource Acquisition Is Initialization) pattern. The recommended approach is to use a `using` statement, which ensures that the stream is properly disposed of when you're done with it, even if an exception occurs. Alternatively, you can manually call `Dispose()` on the `EventStream` object when finished.

The `EventStream` instance can be consumed by repeatedly calling `Next()` until it returns null, indicating the end of the stream.

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
<!-- End Server-sent event streaming [eventstream] -->

<!-- Start Error Handling [errors] -->
## Error Handling

[`OpenRouterException`](./src/OpenRouterSDK/Models/Errors/OpenRouterException.cs) is the base exception class for all HTTP error responses. It has the following properties:

| Property      | Type                  | Description           |
|---------------|-----------------------|-----------------------|
| `Message`     | *string*              | Error message         |
| `Request`     | *HttpRequestMessage*  | HTTP request object   |
| `Response`    | *HttpResponseMessage* | HTTP response object  |

Some exceptions in this SDK include an additional `Payload` field, which will contain deserialized custom error data when present. Possible exceptions are listed in the [Error Classes](#error-classes) section.

### Example

```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Errors;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    httpReferer: "<value>",
    xTitle: "<value>",
    apiKey: "<YOUR_BEARER_TOKEN_HERE>"
);

try
{
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
}
catch (OpenRouterException ex) // all SDK exceptions inherit from OpenRouterException
{
    // ex.ToString() provides a detailed error message
    System.Console.WriteLine(ex);

    // Base exception fields
    HttpRequestMessage request = ex.Request;
    HttpResponseMessage response = ex.Response;
    var statusCode = (int)response.StatusCode;
    var responseBody = ex.Body;

    if (ex is BadRequestResponseException) // different exceptions may be thrown depending on the method
    {
        // Check error data fields
        BadRequestResponseExceptionPayload payload = ex.Payload;
        BadRequestResponseErrorData Error = payload.Error;
        string UserId = payload.UserId;
        // ...
    }

    // An underlying cause may be provided
    if (ex.InnerException != null)
    {
        Exception cause = ex.InnerException;
    }
}
catch (OperationCanceledException ex)
{
    // CancellationToken was cancelled
}
catch (System.Net.Http.HttpRequestException ex)
{
    // Check ex.InnerException for Network connectivity errors
}
```

### Error Classes

**Primary exceptions:**
* [`OpenRouterException`](./src/OpenRouterSDK/Models/Errors/OpenRouterException.cs): The base class for HTTP error responses.
  * [`InternalServerResponseException`](./src/OpenRouterSDK/Models/Errors/InternalServerResponseException.cs): Internal Server Error - Unexpected server error. Status code `500`.
  * [`UnauthorizedResponseException`](./src/OpenRouterSDK/Models/Errors/UnauthorizedResponseException.cs): Unauthorized - Authentication required or invalid credentials. Status code `401`. *

<details><summary>Less common exceptions (14)</summary>

* [`System.Net.Http.HttpRequestException`](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.httprequestexception): Network connectivity error. For more details about the underlying cause, inspect the `ex.InnerException`.

* Inheriting from [`OpenRouterException`](./src/OpenRouterSDK/Models/Errors/OpenRouterException.cs):
  * [`NotFoundResponseException`](./src/OpenRouterSDK/Models/Errors/NotFoundResponseException.cs): Not Found - Resource does not exist. Status code `404`. Applicable to 18 of 35 methods.*
  * [`BadRequestResponseException`](./src/OpenRouterSDK/Models/Errors/BadRequestResponseException.cs): Bad Request - Invalid request parameters or malformed input. Status code `400`. Applicable to 17 of 35 methods.*
  * [`TooManyRequestsResponseException`](./src/OpenRouterSDK/Models/Errors/TooManyRequestsResponseException.cs): Too Many Requests - Rate limit exceeded. Status code `429`. Applicable to 10 of 35 methods.*
  * [`PaymentRequiredResponseException`](./src/OpenRouterSDK/Models/Errors/PaymentRequiredResponseException.cs): Payment Required - Insufficient credits or quota to complete request. Status code `402`. Applicable to 4 of 35 methods.*
  * [`BadGatewayResponseException`](./src/OpenRouterSDK/Models/Errors/BadGatewayResponseException.cs): Bad Gateway - Provider/upstream API failure. Status code `502`. Applicable to 4 of 35 methods.*
  * [`EdgeNetworkTimeoutResponseException`](./src/OpenRouterSDK/Models/Errors/EdgeNetworkTimeoutResponseException.cs): Infrastructure Timeout - Provider request timed out at edge network. Status code `524`. Applicable to 4 of 35 methods.*
  * [`ProviderOverloadedResponseException`](./src/OpenRouterSDK/Models/Errors/ProviderOverloadedResponseException.cs): Provider Overloaded - Provider is temporarily overloaded. Status code `529`. Applicable to 4 of 35 methods.*
  * [`ForbiddenResponseException`](./src/OpenRouterSDK/Models/Errors/ForbiddenResponseException.cs): Forbidden - Authentication successful but insufficient permissions. Status code `403`. Applicable to 3 of 35 methods.*
  * [`ServiceUnavailableResponseException`](./src/OpenRouterSDK/Models/Errors/ServiceUnavailableResponseException.cs): Service Unavailable - Service temporarily unavailable. Status code `503`. Applicable to 3 of 35 methods.*
  * [`RequestTimeoutResponseException`](./src/OpenRouterSDK/Models/Errors/RequestTimeoutResponseException.cs): Request Timeout - Operation exceeded time limit. Status code `408`. Applicable to 2 of 35 methods.*
  * [`PayloadTooLargeResponseException`](./src/OpenRouterSDK/Models/Errors/PayloadTooLargeResponseException.cs): Payload Too Large - Request payload exceeds size limits. Status code `413`. Applicable to 2 of 35 methods.*
  * [`UnprocessableEntityResponseException`](./src/OpenRouterSDK/Models/Errors/UnprocessableEntityResponseException.cs): Unprocessable Entity - Semantic validation failure. Status code `422`. Applicable to 2 of 35 methods.*
  * [`ResponseValidationError`](./src/OpenRouterSDK/Models/Errors/ResponseValidationError.cs): Thrown when the response data could not be deserialized into the expected type.
</details>

\* Refer to the [relevant documentation](#available-resources-and-operations) to determine whether an exception applies to a specific operation.
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Name

You can override the default server globally by passing a server name to the `server: string` optional parameter when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the names associated with the available servers:

| Name         | Server                         | Description       |
| ------------ | ------------------------------ | ----------------- |
| `production` | `https://openrouter.ai/api/v1` | Production server |

#### Example

```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    server: SDKConfig.Server.Production,
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

### Override Server URL Per-Client

The default server can also be overridden globally by passing a URL to the `serverUrl: string` optional parameter when initializing the SDK client instance. For example:
```csharp
using OpenRouterSDK;
using OpenRouterSDK.Models.Components;
using OpenRouterSDK.Models.Requests;

var sdk = new OpenRouter(
    serverUrl: "https://openrouter.ai/api/v1",
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
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The C# SDK makes API calls using an `ISpeakeasyHttpClient` that wraps the native
[HttpClient](https://docs.microsoft.com/en-us/dotnet/api/system.net.http.httpclient). This
client provides the ability to attach hooks around the request lifecycle that can be used to modify the request or handle
errors and response.

The `ISpeakeasyHttpClient` interface allows you to either use the default `SpeakeasyHttpClient` that comes with the SDK,
or provide your own custom implementation with customized configuration such as custom message handlers, timeouts,
connection pooling, and other HTTP client settings.

The following example shows how to create a custom HTTP client with request modification and error handling:

```csharp
using OpenRouterSDK;
using OpenRouterSDK.Utils;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;

// Create a custom HTTP client
public class CustomHttpClient : ISpeakeasyHttpClient
{
    private readonly ISpeakeasyHttpClient _defaultClient;

    public CustomHttpClient()
    {
        _defaultClient = new SpeakeasyHttpClient();
    }

    public async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken? cancellationToken = null)
    {
        // Add custom header and timeout
        request.Headers.Add("x-custom-header", "custom value");
        request.Headers.Add("x-request-timeout", "30");
        
        try
        {
            var response = await _defaultClient.SendAsync(request, cancellationToken);
            // Log successful response
            Console.WriteLine($"Request successful: {response.StatusCode}");
            return response;
        }
        catch (Exception error)
        {
            // Log error
            Console.WriteLine($"Request failed: {error.Message}");
            throw;
        }
    }

    public void Dispose()
    {
        _httpClient?.Dispose();
        _defaultClient?.Dispose();
    }
}

// Use the custom HTTP client with the SDK
var customHttpClient = new CustomHttpClient();
var sdk = new OpenRouter(client: customHttpClient);
```

<details>
<summary>You can also provide a completely custom HTTP client with your own configuration:</summary>

```csharp
using OpenRouterSDK.Utils;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;

// Custom HTTP client with custom configuration
public class AdvancedHttpClient : ISpeakeasyHttpClient
{
    private readonly HttpClient _httpClient;

    public AdvancedHttpClient()
    {
        var handler = new HttpClientHandler()
        {
            MaxConnectionsPerServer = 10,
            // ServerCertificateCustomValidationCallback = customCertValidation, // Custom SSL validation if needed
        };

        _httpClient = new HttpClient(handler)
        {
            Timeout = TimeSpan.FromSeconds(30)
        };
    }

    public async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken? cancellationToken = null)
    {
        return await _httpClient.SendAsync(request, cancellationToken ?? CancellationToken.None);
    }

    public void Dispose()
    {
        _httpClient?.Dispose();
    }
}

var sdk = OpenRouter.Builder()
    .WithClient(new AdvancedHttpClient())
    .Build();
```
</details>

<details>
<summary>For simple debugging, you can enable request/response logging by implementing a custom client:</summary>

```csharp
public class LoggingHttpClient : ISpeakeasyHttpClient
{
    private readonly ISpeakeasyHttpClient _innerClient;

    public LoggingHttpClient(ISpeakeasyHttpClient innerClient = null)
    {
        _innerClient = innerClient ?? new SpeakeasyHttpClient();
    }

    public async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken? cancellationToken = null)
    {
        // Log request
        Console.WriteLine($"Sending {request.Method} request to {request.RequestUri}");
        
        var response = await _innerClient.SendAsync(request, cancellationToken);
        
        // Log response
        Console.WriteLine($"Received {response.StatusCode} response");
        
        return response;
    }

    public void Dispose() => _innerClient?.Dispose();
}

var sdk = new OpenRouter(client: new LoggingHttpClient());
```
</details>

The SDK also provides built-in hook support through the `SDKConfiguration.Hooks` system, which automatically handles
`BeforeRequestAsync`, `AfterSuccessAsync`, and `AfterErrorAsync` hooks for advanced request lifecycle management.
<!-- End Custom HTTP Client [http-client] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=open-router-sdk&utm_campaign=csharp)
