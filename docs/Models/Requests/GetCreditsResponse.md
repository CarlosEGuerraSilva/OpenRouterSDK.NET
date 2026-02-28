# GetCreditsResponse


## Fields

| Field                                                                     | Type                                                                      | Required                                                                  | Description                                                               | Example                                                                   |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `HttpMeta`                                                                | [HTTPMetadata](../../Models/Components/HTTPMetadata.md)                   | :heavy_check_mark:                                                        | N/A                                                                       |                                                                           |
| `Object`                                                                  | [GetCreditsResponseBody](../../Models/Requests/GetCreditsResponseBody.md) | :heavy_minus_sign:                                                        | Returns the total credits purchased and used                              | {<br/>"data": {<br/>"total_credits": 100.5,<br/>"total_usage": 25.75<br/>}<br/>} |