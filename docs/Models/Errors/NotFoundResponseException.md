# NotFoundResponseException

Not Found - Resource does not exist


## Fields

| Field                                                                             | Type                                                                              | Required                                                                          | Description                                                                       | Example                                                                           |
| --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `Error`                                                                           | [NotFoundResponseErrorData](../../Models/Components/NotFoundResponseErrorData.md) | :heavy_check_mark:                                                                | Error data for NotFoundResponse                                                   | {<br/>"code": 404,<br/>"message": "Resource not found"<br/>}                      |
| `UserId`                                                                          | *string*                                                                          | :heavy_minus_sign:                                                                | N/A                                                                               |                                                                                   |
| `HttpMeta`                                                                        | [HTTPMetadata](../../Models/Components/HTTPMetadata.md)                           | :heavy_check_mark:                                                                | N/A                                                                               |                                                                                   |