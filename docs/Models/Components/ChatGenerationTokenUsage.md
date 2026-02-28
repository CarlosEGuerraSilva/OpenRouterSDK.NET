# ChatGenerationTokenUsage

Token usage statistics


## Fields

| Field                                                                         | Type                                                                          | Required                                                                      | Description                                                                   |
| ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `CompletionTokens`                                                            | *double*                                                                      | :heavy_check_mark:                                                            | Number of tokens in the completion                                            |
| `PromptTokens`                                                                | *double*                                                                      | :heavy_check_mark:                                                            | Number of tokens in the prompt                                                |
| `TotalTokens`                                                                 | *double*                                                                      | :heavy_check_mark:                                                            | Total number of tokens                                                        |
| `CompletionTokensDetails`                                                     | [CompletionTokensDetails](../../Models/Components/CompletionTokensDetails.md) | :heavy_minus_sign:                                                            | Detailed completion token usage                                               |
| `PromptTokensDetails`                                                         | [PromptTokensDetails](../../Models/Components/PromptTokensDetails.md)         | :heavy_minus_sign:                                                            | Detailed prompt token usage                                                   |