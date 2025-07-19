You will be given the **components.schemas** section from an `OpenAPI 3.0` document for project `fm_project_name`. Your job is to:

1. Generate a TypeScript `interface` or `type` for each schema.
2. Preserve:
   - Required vs optional properties
   - Enum values
   - Nested objects and arrays
   - Descriptions (as comments if available)
3. If a schema uses `$ref` to reference another schema, use the appropriate TypeScript type name (assume they will all be present).
4. Use native types (`string`, `number`, `boolean`, `Date`, etc.) when appropriate.
5. Add `readonly` to `readOnly: true` fields.
6. Generate idiomatic, clean TypeScript code.

Here is the `components.schemas` JSON:

fm_openapi_specs

```json
{
   "result": 
   {
        "server/src/types/types.ts":"typescript types based on the components",
        "general_notes":" Any notes about about the types? any things to consider for the developer who is going to use this especially if needs improvement. "
    }
}
```
