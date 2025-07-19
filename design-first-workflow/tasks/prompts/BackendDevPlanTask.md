## Your Task

You are in charge of preparing a detailed, step-by-step **Plan** for building a **production-grade API**. You are working under the direction of your tech lead, who has already provided:

- A **complete and finalized OpenAPI specification** (MUST NOT BE CHANGED)
- A **technical architecture design**, expressed as a folder structure with notes

This project follows an **OpenAPI-first** and **TDD-driven** development methodology.

---

## Input #1 – the **OpenAPI specification**

Here is the completed **OpenAPI document** that will be available in the repository already.

fm_specs


## Input #2 – Architecture Design

You are also given a technical folder structure proposed by the tech lead. It provides guidance for where different components should be placed.

📁 Use `fm_architecture_design` to refer to the architectural layout and organization rules.

fm_folder_structure
---

During the development, you will always get the **updated state** of the project repository which begins with the **OpenAPI specification** in `openapi.json`and then it gets updated with **your generated files**.

## Instructions for Developing the Plan

Your output should be a **step-by-step plan**, where each step represents a logical **development increment**.

- Each increment will correspond to a **pull request** made to a shared Git repository.
- Each increment must be:
  - **Logically self-contained**
  - **Testable**
  - Aligned with the **OpenAPI spec** 
- The **output of each increment** becomes **input for the next**—your plan should reflect this progressive buildup.
- List the `validation_commands` that can be used to **validate the result** of a specific increment. 
      >> **Any listed commands should work after each the increment. If no commands work then, then leave the array empty**
- The plan must eventually include using all the response and request examples and scenarios in building **integration test coverage** for all endpoints 

---

## Guidelines

✅ Start with `configuration and setup` to ensure `npm start` works without errors  
✅ Get the models layer done early and get it to match the `Components schema` in the OpenAPI document.
✅ Integration tests must cover **all OpenAPI endpoints**, using examples for realism  
✅ **Test File Structure for Endpoints**
   * Integration tests must be split according to the endpoint path convention:
     * A separate file for `/resources`
     * A separate file for `/resources/:id`

✅ **OpenAPI Document Handling**
   * The `openapi.json` file is **already provided in the repository** and is **considered finalized**.
   * **Do not include any steps to add, modify, or move the OpenAPI file.**
   * Using tools like `swagger-ui-express` and `express-openapi-validator` can be part of the setup but should be **combined with the server entry files (index.js and app.js)** 

✅  **Architecture Flexibility**

   * The architecture (`fm_architecture_design`) is the **base guideline**, not a constraint.
   * You may **introduce additional files, modules, or helper folders** (e.g., for config, utils, or constants) if they are justified by **best practices** for the selected technology stack.
   * All such additions should clearly support and align with the overall architecture and the current development increment’s goal.


---

## 🧾 Output Format

Return a JSON array of increment objects. Each object should include:

>> state the **exact file names** and full path in each increments.

```json
[
  {
    "increment_title": "Setup and configuration",
    "increment_summary_description": "What this increment introduces or changes, used as the PR description.",
    "openapi_elements": "List any related OpenAPI Components, paths and operations (e.g., GET /badges)",
    "target_files": [
      { "path/to/file.js": "Purpose of this file" }
      ],
    "validation_commands":["`npm start`", "curl ...", ""]  // validation commands must work without errors after an increment. If no commands work yet, leave it empty.
  }
]
````
