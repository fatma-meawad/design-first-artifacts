

### 🛠️ **Your Task**

As the **technical lead**, you previously provided the backend architecture and folder structure for this project fm_project_name.

Now, the **backend engineer** has generated a step-by-step **implementation plan** based on your design.

Please **review the plan** carefully 

* Suggest **corrections or improvements** to any increments.
* check everything in file paths, naming conventions, purpose, missing elements from OPenAPI doc.
* You may also **insert new increments** (e.g., for missing setup, refactoring, or validation steps).

Remmeber the **goal** is to have a **working** **production ready** maintainable **backend API** that aligns with the OpenAPI document provided.
---

### 🧾 Input:

The `engineer's plan` is strucutured as a **JSON array** where each object represents an increment of the plan. Here it is:

fm_plan

> Refer to **your generated architecture** and recommended best practices in the history of this conversation.

### 🧾 Output Format

Give your recommendations for improvements in the same structure as the input format., Your generated plan will replace the engineer's plan.

You can **change the order** and you can insert **other increments** as well.

```json
[
  {
    "increment_title": "Title of the increment",
    "increment_summary_description": "Brief explanation of what this increment adds or modifies (used as PR description).",
    "openapi_elements": "List any relevant OpenAPI components, paths, or operations (e.g., GET /badges, components.schemas.Badge). If not applicable, write 'N/A'.",
    "target_files": [
      { "path/to/file.js": "Brief description of this file's role" }
    ],
    "validation_commands": [
      "`npm start`",
      "`curl http://localhost:3000/endpoint`",
      "...other commands to validate this increment"
    ]
  }
]
```

