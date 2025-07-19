### 📋 **Your Task**

> Your first task as a tech lead is to define the **technical development plan** needed to evolve the `repository state` for `server` shared with you into a `fully functional, tested, and production-ready API` — without redoing what’s already scaffolded.

---
### ✅ **Guidelines for Completing the Backend**

#### 1. 🧰 **Infrastructure & Environment**

* Set up **Docker** for local development:

  * Include `Dockerfile` and `docker-compose.yml` to spin up the backend and database (MongoDB).
  * Mount volumes and enable hot reload in development mode (`npm run dev`).
  * All configs (port, DB URI, logging) should be accessed via require('./lib/config').
  * Manage **environment variables** properly for docker-compose: the database and the backend
  * Database connection should be handled gracefully for testing and production
  * At the moment, **all the scripts** in `package.json` work, make sure your **changes don't break** the scripts.
  * The `.env` file currently in the root folder is the default one for `development` phase.
  

#### 2. 📦 **Models/Data Layer**

Use `Mongoose` for using MongoDB
* Reflect the `OpenAPI components schemas` in the `OpenAPI document` to `Mongoose schema`. The OpenAPI types, format and validation is the source of truth.
* Start by getting the models done to build over it the rest of the decisions.
* Add all **operations** to the models that will be needed by for `the end points` in the `OpenAPI specification` file, for example , like listing, finding, etc.
* Make sure the **database connection** is handled for graceful handling  (open and close) in different environemnts `development`, `production` and `testing` is handled.

#### 3. 🔐 **Security & Auth**

* Wire up the **OAuth2 flow** placeholders (e.g., GitHub/Gmail login).
* Respect OpenAPI security rules (e.g., `/resources` POST/PUT/DELETE require authorization).
* Add `middleware` in routes, to protect `specific routes` that are protected by securty schema.
* Add `middleware` to inject authenticated user info into requests.

#### 4. 🧪 **Complete Integration Tests**

* Use the existing skeletons in `server/tests/*.js` to:

  * Test each endpoint against the OpenAPI contract
  * Use `supertest` to mock real requests
  * Validate error codes (e.g., `400`, `401`) using invalid **input examples** from the spec
  * `Don't add tests` for the `500` errors or for server crashes. Just cover logical errors for the application.
  * Always refer to the `OpenAPI schema components types` and formatting in the assertions checks.


#### 5. 🧱 **Complete Business Logic**

* Implement actual logic inside the `services/*.js` files.
* Avoid logic in `controllers` or `routes`. Route handlers should remain thin.
* Use the schema definitions as ground truth for validating structure and required fields.
* 🔁 **Follow OpenAPI for Input/Output**
* Ensure services return `data shapes` aligned with the `OpenAPI examples`.
* Maintain consistent `status codes` and error formats as defined in the `responses` section.
* Make use of example values in the OpenAPI doc as fixtures for testing.
* Always refer to the `OpenAPI schema components types` and formatting in the assertions checks.


#### 6. 🧱 **Configuration file usage check**

Dedicate a `whole increment` to check the proper use of the config object across all files `src\lib\config.js`:
* All required configuration variables need across the API should be added to `.env`, `.env.production`, `.env.test`
* Then any layer (models, database, server port, test, routers, etc) that is using the `configuration variables` should be using `config` from  `src\lib\config.js` to access the configuration variables
* `process.env` should not be used directly in code.
* With this setting in place, starting the API in development, test or production will help config to load the right `environment variable` file.

#### 7. 🧱 **Authentication and Authorization Middleware**

Dedicate a `whole increment` to check the proper use of the authentication and authorization middleware`:
* Make sure the `authentication middleware` is applied to the respective `routes`
* Actions that must be protected by authentication, should be protected by the authentication middlewar check.
* Actions that requires access control or permission should be protected by the authorization checks.
* Any `/login` or `/signup` routes should be public to allow unregistered users to join in.

#### 8. 🧱 **Integration tests**

Dedicate a `whole increment` to check the proper design of `integration tests`:
* Integration `tests assertions` should match what `services layer` return in each respective scenario.
* Make sure the attributes used in tests match the attributes used in the code
* Always refer to the `OpenAPI schema components types` and formatting.
* 🔁 **Follow OpenAPI for Input/Output**


#### 9. 🧱 **Wrap up and review**
Dedicate a `whole increment` for a final review of the code:           
* check all `dependencies` and package imports are in the right place
* Make sure source code is all in `src` folder
* Ensure `tests for all endpoints` are present and validate the requests and responses (including examples) as defined in the OpenAPI spec.
* Check that the `database connection` and configurations are corretly setup. 
* Make sure the `configurations and layers` of the original generated code are used and not duplicated in a different way, for example, loggere and error objects.

#### **General Rules**

* Don’t duplicate validation — use `express-openapi-validator` where possible. So don't do manual validation for request handlers.
* Implement schema-level checks in your models (e.g., title uniqueness).
* Ensure `lib/error.js` and logging are consistently used.
* ❌ **Avoid Redundancy**
* Don't rewrite files already scaffolded (e.g., route files, placeholder functions).
* The current skeleton files have some **coding tips** commented inside functions, check those out as well for some ideas.

## 🧾 Output Format

- Return a `JSON array` of increment objects.  
- Cover `all development aspects` discussed above generating an Increment specially for each concept.
- Each increment object should include:


```json
[
  {
    "increment_title": "title of the increment",
    "increment_summary_description": "What this increment introduces or changes, used as the PR description.",
    "openapi_elements": "List any related OpenAPI Components, paths and operations (e.g., GET /items)",
    "target_files": [
      { "path/to/file.js": "give full path of the file and here the Purpose of this file. Give good description and be detailed about what should go in here refering to the tips shared above" }
      ],
    "validation_commands":["`npm start`", "curl ...", ""]  // validation commands must work without errors after an increment. If no commands work yet, leave it empty.
  }
]

```