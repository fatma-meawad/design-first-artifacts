**Objective:** Generate `fm_stack` API components following these strict `Clean Architecture patterns` 

## Directory Structure:

Here is the directory structure of the target repository

```bash
src/
  features/
    {resource}/          # e.g., todos/
      domain/
        entities/        # Business objects 
        dtos/            # Data Transfer Objects  
        repositories/    # Abstract interfaces
        usecases/        # Business logic   (paths for this reosurce)
        datasources/     # Data source interfaces
      infrastructure/    # Implementations
      presentation/      # Controllers & routes
```

---

## high level architecture diagram 

The following diagram shows the main layers and the flow between them in the  target clean architecture repository

```mermaid

%% High-level component diagram
graph TD
    subgraph Presentation Layer
        A[Controller] -->|Uses| B[Use Cases]
        C[Routes] -->|Initializes| A
        C -->|Uses| D[Error Middleware]
    end

    subgraph Domain Layer
        B -->|Implements| E[Repository Interfaces]
        B -->|Uses| F[Entities]
        B -->|Uses| G[DTOs]
    end

    subgraph Infrastructure Layer
        E -->|Implemented by| H[Repository Impl]
        H -->|Uses| I[Data Sources]
        I -->|Can be| J[Database]
        I -->|Can be| K[API]
        I -->|Can be| L[In-Memory]
    end
```

## Here is a class diagram with a focus on the details of different classes.

```mermaid
classDiagram
    %% Layer 1: Presentation
    class TodoController {
        -repository: TodoRepository
        +getAll(req: Request, res: Response): void
        +create(req: Request, res: Response): void
    }

    class TodoRoutes {
        +static routes(): Router
    }

    %% Layer 2: Domain
    class TodoEntity {
        +id: number
        +text: string
        +isCompleted: boolean
        +static fromJson(obj: any)$ TodoEntity
    }

    class CreateTodoDto {
        +text: string
        +static create(obj: any)$ CreateTodoDto
        -validate() void
    }

    class TodoRepository {
        <<interface>>
        +getAll()$ Promise~TodoEntity[]~
        +create(dto: CreateTodoDto)$ Promise~TodoEntity~
    }

    class GetTodosUseCase {
        -repository: TodoRepository
        +execute()$ Promise~TodoEntity[]~
    }

    %% Layer 3: Infrastructure
    class TodoRepositoryImpl {
        -datasource: TodoDatasource
        +getAll()$ Promise~TodoEntity[]~
    }

    class TodoDatasourceImpl {
        -todos: TodoEntity[]
        +getAll()$ Promise~TodoEntity[]~
    }

    %% Layer Boundaries
    PresentationLayer --|> DomainLayer : Depends on
    DomainLayer --|> InfrastructureLayer : Depends on

    %% Relationships
    TodoRoutes --> TodoController
    TodoController --> GetTodosUseCase
    GetTodosUseCase --> TodoRepository
    TodoRepositoryImpl ..|> TodoRepository
    TodoRepositoryImpl --> TodoDatasourceImpl
    CreateTodoDto --> TodoEntity

    note for PresentationLayer "Handles HTTP:\n- Routes\n- Controllers\n- Middleware"
    note for DomainLayer "Business Logic:\n- Entities\n- Use Cases\n- Interfaces"
    note for InfrastructureLayer "Implementations:\n- Databases\n- External APIs"
```
## Key Principles to Enforce:
1. **Dependency Rule**: Inner layers (domain) must never import outer layers (infrastructure/presentation)
2. **Testability**: All components must be mockable via interfaces
3. **Validation**: Entities/DTOs validate themselves
4. **Error Handling**: Consistent error formats across layers

##  Error Handling

Pattern: Centralized error middleware

```ts
// core/errors/custom.error.ts
class AppError extends Error {
  constructor(
    public readonly statusCode: HttpCode,
    public readonly validationErrors?: { field: string; constraint: string }[]
  ) {}
}

// presentation/middlewares/error.middleware.ts
function handleError(error: unknown, res: Response) {
  if (error instanceof AppError) {
    res.status(error.statusCode).json({
      error: error.message,
      details: error.validationErrors
    });
  }
}
```

##  Validation Types

Centralized Validation types used by all

```ts
// core/types/index.ts
export interface ValidationType {
	fields: string[];
	constraint: string;
}

export interface SuccessResponse<T> {
	data?: T;
}

export interface ErrorResponse {
	name: string;
	message: string;
	validationErrors?: ValidationType[];
	stack?: string;
}
```

## Input: The OpenAPI spec file: 

Here is the specs: `openapi.json` for the project: `fm_project_name`:

fm_openapi_specs
