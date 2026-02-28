# ChatMessageTokenLogprobs

Log probabilities for the completion


## Fields

| Field                                                                               | Type                                                                                | Required                                                                            | Description                                                                         |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `Content`                                                                           | List<[ChatMessageTokenLogprob](../../Models/Components/ChatMessageTokenLogprob.md)> | :heavy_check_mark:                                                                  | Log probabilities for content tokens                                                |
| `Refusal`                                                                           | List<[ChatMessageTokenLogprob](../../Models/Components/ChatMessageTokenLogprob.md)> | :heavy_check_mark:                                                                  | Log probabilities for refusal tokens                                                |