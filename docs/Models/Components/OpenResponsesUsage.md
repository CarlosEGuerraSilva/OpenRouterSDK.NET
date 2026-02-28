# OpenResponsesUsage

Token usage information for the response


## Fields

| Field                                                                 | Type                                                                  | Required                                                              | Description                                                           |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `InputTokens`                                                         | *double*                                                              | :heavy_check_mark:                                                    | N/A                                                                   |
| `InputTokensDetails`                                                  | [InputTokensDetails](../../Models/Components/InputTokensDetails.md)   | :heavy_check_mark:                                                    | N/A                                                                   |
| `OutputTokens`                                                        | *double*                                                              | :heavy_check_mark:                                                    | N/A                                                                   |
| `OutputTokensDetails`                                                 | [OutputTokensDetails](../../Models/Components/OutputTokensDetails.md) | :heavy_check_mark:                                                    | N/A                                                                   |
| `TotalTokens`                                                         | *double*                                                              | :heavy_check_mark:                                                    | N/A                                                                   |
| `Cost`                                                                | *double*                                                              | :heavy_minus_sign:                                                    | Cost of the completion                                                |
| `IsByok`                                                              | *bool*                                                                | :heavy_minus_sign:                                                    | Whether a request was made using a Bring Your Own Key configuration   |
| `CostDetails`                                                         | [CostDetails](../../Models/Components/CostDetails.md)                 | :heavy_minus_sign:                                                    | N/A                                                                   |