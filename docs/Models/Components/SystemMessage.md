# SystemMessage

System message for setting behavior


## Fields

| Field                                                                   | Type                                                                    | Required                                                                | Description                                                             | Example                                                                 |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `Role`                                                                  | [SystemMessageRole](../../Models/Components/SystemMessageRole.md)       | :heavy_check_mark:                                                      | N/A                                                                     |                                                                         |
| `Content`                                                               | [SystemMessageContent](../../Models/Components/SystemMessageContent.md) | :heavy_check_mark:                                                      | System message content                                                  | You are a helpful assistant.                                            |
| `Name`                                                                  | *string*                                                                | :heavy_minus_sign:                                                      | Optional name for the system message                                    | Assistant Config                                                        |