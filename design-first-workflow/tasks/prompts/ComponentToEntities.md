

## Your task
Generate the `Entities` for the resources in the `components.schema` of the attached OpenAPI specs `openapi.json` with:
1. Strict separation of concerns as defined earlier in your `goal` in this conversation. 
2. The `domain layer` is framework agnostic and has pure business logic.
3. TypeScript types for all inputs/outputs
4. Validation matching the `OpenAPI specs` in `openapi.json`
5. Error handling using `AppError` pattern
6. `JSDoc` explaining each method's purpose

## Guidelines
Our focus in this request is on the the `Entities`:

### How to create the **Entities**
   - Represent core business objects
   - Must include:
     - TypeScript class with constructor
     - `static fromJson()` for validation
     - Strict property typing
   - Example:

     ```typescript
     import { AppError, ZERO } from '../../../../core'; //ZERO is a constant value of ZERO

     class TodoEntity {
       constructor(
         public id: number,
         public text: string,
         public isCompleted: boolean = false
       ) {}
       
       static fromJson(obj: Record<string, unknown>) {
         if (!obj.id) throw AppError.badRequest("ID required");
         return new TodoEntity(obj.id as number, obj.text as string);
       }
     }
     ```


## Important Notes:

1. Any `weak entities` should be separated as a `separate` entity. This can be seen in the `component.schema` is a component referencing another component schema as a `1 to many` relation.


## Output Format

```json
{
   "generated_files": 
   {
        "full/path/filename":"the content of the file",
       "full/path/filename":"the content of the file"
   },
    "general_notes": [
    "description of what was done", "possible limitation, practices done"
    ]
}
```
