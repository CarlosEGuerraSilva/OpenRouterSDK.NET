# ChatGenerationParamsTrace

Metadata for observability and tracing. Known keys (trace_id, trace_name, span_name, generation_name, parent_span_id) have special handling. Additional keys are passed through as custom metadata to configured broadcast destinations.


## Fields

| Field                        | Type                         | Required                     | Description                  |
| ---------------------------- | ---------------------------- | ---------------------------- | ---------------------------- |
| `TraceId`                    | *string*                     | :heavy_minus_sign:           | N/A                          |
| `TraceName`                  | *string*                     | :heavy_minus_sign:           | N/A                          |
| `SpanName`                   | *string*                     | :heavy_minus_sign:           | N/A                          |
| `GenerationName`             | *string*                     | :heavy_minus_sign:           | N/A                          |
| `ParentSpanId`               | *string*                     | :heavy_minus_sign:           | N/A                          |
| `AdditionalProperties`       | Dictionary<String, *object*> | :heavy_minus_sign:           | N/A                          |