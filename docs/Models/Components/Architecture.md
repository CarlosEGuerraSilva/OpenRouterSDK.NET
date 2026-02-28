# Architecture

Model architecture information


## Fields

| Field                                                             | Type                                                              | Required                                                          | Description                                                       | Example                                                           |
| ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| `Tokenizer`                                                       | [Tokenizer](../../Models/Components/Tokenizer.md)                 | :heavy_check_mark:                                                | N/A                                                               | GPT                                                               |
| `InstructType`                                                    | [InstructType](../../Models/Components/InstructType.md)           | :heavy_check_mark:                                                | Instruction format type                                           |                                                                   |
| `Modality`                                                        | *string*                                                          | :heavy_check_mark:                                                | Primary modality of the model                                     | text                                                              |
| `InputModalities`                                                 | List<[InputModality](../../Models/Components/InputModality.md)>   | :heavy_check_mark:                                                | Supported input modalities                                        |                                                                   |
| `OutputModalities`                                                | List<[OutputModality](../../Models/Components/OutputModality.md)> | :heavy_check_mark:                                                | Supported output modalities                                       |                                                                   |