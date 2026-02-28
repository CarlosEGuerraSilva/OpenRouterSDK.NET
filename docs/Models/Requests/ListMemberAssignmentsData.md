# ListMemberAssignmentsData


## Fields

| Field                                                 | Type                                                  | Required                                              | Description                                           | Example                                               |
| ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- | ----------------------------------------------------- |
| `Id`                                                  | *string*                                              | :heavy_check_mark:                                    | Unique identifier for the assignment                  | 550e8400-e29b-41d4-a716-446655440000                  |
| `UserId`                                              | *string*                                              | :heavy_check_mark:                                    | Clerk user ID of the assigned member                  | user_abc123                                           |
| `OrganizationId`                                      | *string*                                              | :heavy_check_mark:                                    | Organization ID                                       | org_xyz789                                            |
| `GuardrailId`                                         | *string*                                              | :heavy_check_mark:                                    | ID of the guardrail                                   | 550e8400-e29b-41d4-a716-446655440001                  |
| `AssignedBy`                                          | *string*                                              | :heavy_check_mark:                                    | User ID of who made the assignment                    | user_abc123                                           |
| `CreatedAt`                                           | *string*                                              | :heavy_check_mark:                                    | ISO 8601 timestamp of when the assignment was created | 2025-08-24T10:30:00Z                                  |