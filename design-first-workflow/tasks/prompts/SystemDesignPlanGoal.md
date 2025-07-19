### 🗂️ **Your Goal**

You are leading a team to build a **production-grade API** based on a **complete OpenAPI specification** for project: `fm_project_name`.
You are given an initial repository, which is a backend API project scaffolded using **swagger-node-codegen** based on a complete OpenAPI 3.0 specification for the project.

---

## Here is an overview of the 📁 Folder Structure :

```bash
server/
├── .env                    # Development environment variables
├── docs/
│   └── openapi.json        # OpenAPI spec (source of truth for all endpoints)
├── package.json            # Project metadata and scripts
├── tests/                  # Jest + Supertest integration tests
│   ├── badges.js
│   └── login.js
└── src/
    ├── bin/
    │   └── www             # App entrypoint (HTTP server)
    ├── lib/                # Core shared utilities
    │   ├── config.js       # Loads the correct .env.* config file into one `config` object
    │   ├── error.js        # Custom `ServerError` class for consistent error formatting
    │   └── logger.js       # Bunyan-based logger using config-driven levels
    ├── routes/             # Express routes mapped to OpenAPI endpoints
    │   ├── badges.js
    │   └── login.js
    ├── services/           # Business logic separated from routing
    │   ├── badges.js
    │   └── login.js
    └── index.js            # App configuration: middlewares, OpenAPI validation, and route mounting

```
---

## 🧱 Layered Architecture

### 1. **API Contract (📁 `docs/`)**

* **Purpose**: Acts as the single source of truth for routes, schemas, validation, and expected behavior.
* **File**: `openapi.json` defines endpoints, request/response shapes, OAuth2 flows, and error schemas.
* **Best Practice**: The rest of the app (routes, tests, validators) should be kept in sync with this file.

---

### 2. **Entrypoint Layer (📁 `src/bin/`)**

* **File**: `www`
* **Purpose**: Starts the HTTP server, sets port, handles low-level server errors.
* **Best Practice**: This file should remain slim and defer setup to `src/index.js`.

---

### 3. **App Layer (📄 `src/index.js`)**

* **Purpose**: Central express app configuration: loads middleware (body-parser, cookie-parser), connects OpenAPI validator, mounts routes, and configures centralized error handling.
* **Highlights**:

  * Mounts Swagger UI at `/docs`.
  * Integrates `express-openapi-validator` for request/response schema enforcement.

---

### 4. **Route Layer (📁 `routes/`)**

* **Purpose**: Maps OpenAPI endpoints to handler functions, acts as controller.
* **Best Practice**: Should only handle routing and validation handoff; no business logic or DB calls.

---

### 5. **Service Layer (📁 `services/`)**

* **Purpose**: Contains `skeleton functions` for core business logic per operation, mostly `CRUD`s. These are `placeholders` and `documentation tips` as comments inside the functions.
* **Best Practice**:
  * Implement data access, authentication and authorization checks using the model layer and processing here.
  * Throw structured errors using `ServerError`.

---

### 6. **Utility Layer (📁 `lib/`)**

* **Files**:

  * `config.js`: Loads and wraps all environment variables using `dotenv`, checks the type of the environment and sets value.
  * `error.js`: Custom centralized `error class` for structured error propagation.
  * `logger.js`: Wraps `bunyan` to provide consistent logging across environments.
* **Purpose**: Shared modules abstracted for reuse and configurability.

---

### 7. **Test Layer (📁 `tests/`)**

* **Purpose**: Contains generated test stubs per endpoint/method using `supertest`.
* **Best Practice**:

  * Flesh these out using real test data and mocks.
  * Validate both happy and error paths as specified in `openapi.json`.

---
### Here is the content of initial `repository state` for `server`


fm_repo_state
