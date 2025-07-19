

## Your task
Generate the `DTOs` for the resources in the `components.schema` of the attached OpenAPI specs `openapi.json` with:
1. Strict separation of concerns as defined earlier in your `goal` in this conversation. 
2. The `domain layer` is framework agnostic and has pure business logic.
3. TypeScript types for all inputs/outputs
4. Validation matching the `OpenAPI specs` in `openapi.json`
5. Error handling using `AppError` pattern
6. `JSDoc` explaining each method's purpose

## Guidelines
Our focus in this request is on the `DTOs`:

### How to build **DTOs (Data Transfer Objects)**?
   - All DTOs must extend CoreDto from shared/domain/dtos/core.dto.ts
   - Validate data between layers
   - Required methods:
     - `static create()`: Factory method
     - `validate()`: Self-validation

   - Example:
     ```typescript

   import { type ValidationType, ZERO, AppError } from '../../../../core';
   import { type CoreDto } from '../../../shared';

    export class CreateTodoDto implements CoreDto<CreateTodoDto> {
      private constructor(public readonly text: string) {
		this.validate(this);
	}
       
    public validate(dto: CreateTodoDto): void {
        ...
    }

    public static create(object: Record<string, unknown>): CreateTodoDto {
         const dto = new CreateTodoDto(obj.text as string);
         dto.validate(dto);
         return dto;
       }
     }
     ```
>> Refer to the generated `entities` in your previous `response`

## Important Notes:


1. All DTOs should follow this validation pattern:
   - Collect all `validation errors` in an array
   - Only throw a single `AppError` at the end if there are any errors
   - Include clear, specific error messages

2. Exact OpenAPI validation (formats, enums, regex)
3. JSDoc with:
   - Property descriptions from spec
   - Example values
   - Validation constraints
4. Error messages that reference OpenAPI rules verbatim
### Required DTO types:
   - CreateTodoDto - for creating todos (requires text)
   - UpdateTodoDto - for updating todos (requires id, optional text/isCompleted)
   - GetTodoByIdDto - for getting single todo (requires id)
   - DeleteTodoDto - for deleting todos (requires id)

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

fm_