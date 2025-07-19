
### 🛠️ **A bit of Context**

As the **technical lead**, you previously planned for the development of the  `fm_project_name` project and reviewed the backend engineer's work. 

### 🛠️ **Your Task**

Your task is to review the `full code content` of the repo after the engineer's has finished the development work. You want to make sure 

1. eveyrthing is `working` as expected (cli commands run without errors )
2. `OpenAPI` specifications are met.
3. `best practices` are followed as given to the engineer in the development process


---

### 🧾 Input 1:

- The `repository files`:


fm_repository_state

> Refer to **the initial repostiroy** for `server` and the suggested best practices.
> Also refere to the `openapi.json` file of OpenAPI specifications.

### 🧾 Input 2:

- Here are the output generated in console after trying running the given command:

fm_errors

### 🧾 Output Format

- ✅ Return the needed corrections/additions to files in the format below (as a pull request of files).

```json

  {
    "generated_corrected_files": {
    "path/to/file.js": {
      "description": "What this file includes or modifies and why. What best practices are followed",
      "content": "Full file content or patch.",
      "state": "new|updated"
    }
  },
"general_notes": [
    "general comments on the code and the best practices", "if the repository code doesn't work, you must identify the changes as major."

]
  }

```



## Development Checklist:

Here is a Here is a checklist to guide your development decisions:
---


### 📜 OpenAPI-Driven Development

* [ ] Use `express-openapi-validator` to enforce compliance with the OpenAPI spec for:
  * [ ] Request validation
  * [ ] Response validation

* By doing this, you don't need to valid request and responses in the code. It is done automatically by the validator.
* Route controllers properly.


### 🧱 Layered Structure (Model – Service – Controller)

#### ✅ Controllers (`controllers/`)

* [ ] Handle HTTP logic only: read from `req`, send via `res`.
* [ ] Call services, format responses.
* [ ] No validation or business logic here if OpenAPI validators are used. They already validate the request/response according to the specs.
* [ ] Add **routing in the server entry** point to route to the right controllers for each request.


#### ✅ Services (`services/`)

* [ ] Contain all **business logic** and calls to DB (via models).
* [ ] Perform **authorization**, sanitization, and cross-model coordination.
* [ ] Handle file uploads/storage logic and persist metadata.
* [ ] No usage of `req`, `res`, or Express here.

#### ✅ Models (`models/`)

* [ ] Define schema validations close to the DB (Mongoose or Prisma).
* [ ] Avoid controller or business logic here.
* [ ] Use virtuals, pre/post hooks, or instance methods only if tied to data behavior.
---

### 🔐 Middleware & Security

* [ ] Include middleware for:

  * [ ] Authentication
  * [ ] Role-based access control (if applicable)
  * [ ] Logging
  * [ ] Error handling
  * [ ] Routing , use the Router Object for routing to controllers.
* [ ] Apply OpenAPI validator **before** hitting the controllers.
* [ ] Secure `.env` variables and avoid hardcoded secrets.

---
### 🔬 Testing

* [ ] Include an integration test suite using **Jest + Supertest**.
* [ ] Test request/response shape against OpenAPI contract.
* [ ] Handle Setup and Teardown properly to avoid leaks and unintended behaviour especially with the database.
* [ ] Use mock data or fixture generators aligned with OpenAPI schema examples.
---

### ⚙️ DevOps & Maintainability

* [ ] Provide CI-ready scripts for:
* [ ] Add linting and formatting config (`eslint`, `prettier`).
  * [ ] Linting
  * [ ] Test execution
  * [ ] Validation against OpenAPI
* [ ] Use `.env-example` and `config/` for DB URIs, upload paths, etc.
* [ ] Include README with full run/setup instructions.
* [ ] Keep `package.json` updated and clean (no vulnerabilities).

---

### 🗃 Recommended Folder/File Structure

* [ ] `index.js` – entrypoint
* [ ] `app.js` – Express setup, middleware, validator, routing
* [ ] `controllers/` – One per resource/domain
* [ ] `services/` – One per domain logic handler
* [ ] `models/` – DB schema files
* [ ] `middleware/` – Reusable logic (e.g., auth, logging)
* [ ] `tests/` – Organized by feature or endpoint
* [ ] `utils/` – Generic helpers
* [ ] `config/` – Environment config
* [ ] `.env-example`, `.gitignore`, `README.md`, etc.

---
### 🔁 Bonus Best Practices

* [ ] Implement **graceful error handling** and standard error format.
* [ ] Use centralized **logging/tracing** (e.g., Winston, Pino).
* [ ] Plan for **API versioning** in routing or URL.
* [ ] Consider **feature-based modularization** for very large APIs.
* [ ] Use patterns and best practices known for the used stack
* [ ] flag redundant code blocks and functionalities.