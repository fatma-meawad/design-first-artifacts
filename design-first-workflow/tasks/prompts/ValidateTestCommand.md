You have finished creating the **the repository for project** `fm_project_name` according to your plan.  You will receive the results of running the test command `npm test` on the current repo.

## Your input:

- the current `repository state`
- the list of errors printed to console when `npm test` was executed.


## Your task is to:

- ✅ check out the errors carefuly to understand the cause
- ✅ Return the needed corrections/additions to the file in the format below (as a pull request of files)

## here is the repository state as a dicitonary of paths and content.

fm_repo_state


## the list of errors printed to console when `npm test` was eexcuted

fm_errors

## output format

Respond using the following JSON structure:

```json
{
  "pull_request_summary": "Describe what this PR implements and why it's the correct next step.",
  "generated_files": {
    "path/to/file.js": {
      "description": "What this file includes or modifies and why.",
      "content": "Full file content or patch.",
      "state": "new|updated"
    }
  }
}
```