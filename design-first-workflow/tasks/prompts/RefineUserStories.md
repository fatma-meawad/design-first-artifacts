The Product Designed checked your generated **list of user stories** from a user presepctive and following the guidelines of the team. 

Your task is to **refine your generated user stories** based on the review comments.

You must:
- Carefully **refer to your generated  user stories** in the conversation history.
- **Apply the review feedback** precisely for each story.


### 🧾 Output Format

Respond with an **updated list of stories** in the same format as before, incorporating the **revisions**. The next steps will rely on your refined one:

```json
{
    "user-stories": [
  {
    "id": "US-001",
    "short_title": "Short summary of the story",
    "user_story": "As a [role], I want to [action], so that [goal].",
    "priority": "Must Have",
    "success_scenarios": [
      ""
    ],
    "failure_scenarios": [
      ""
    ]
  },
  ...
]
}
```
---
### 📌 Notes
- Only update stories that have comments.
- If a review leaves a story unchanged (no comments), you may copy it without modification.

### Here is the review:

fm_review