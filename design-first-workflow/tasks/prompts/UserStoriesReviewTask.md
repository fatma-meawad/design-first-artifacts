## Your task:

The Product Owner generated user stories from the requirements of `fm_project_name`. The product owner would like to get your review. So, You are requested to conduct a **User Acceptance Testing (UAT) Review** of the extracted user stories. Follow the given checklist to help you align with the guidelines of the team as well:

## Input

Here are the extracted `user stories`:

fm_userstories

>> Note that the **original requirements** are in this history of this conversation as well as the **product design document** you have generated.

## **Checklist for UAT Review of User Stories**  

#### **2. Review Each User Story**  
For **every user story** (`US-001`, `US-002`, etc.):  

##### **A. Happy Path (Success Scenarios)**  
✅ Verify:  
- Does it cover the **complete normal flow**?  
- Are **all user inputs** accounted for?  
- Is the **outcome/feedback** clearly described (e.g., "shows success message")?  
- Are **preconditions** explicit (e.g., "Given the user is logged in")?  

##### **B. Failure Scenarios**  
✅ Verify:  
- Are **common user errors** covered (e.g., invalid inputs, missing fields)?  
- Are **edge cases** considered (e.g., **empty lists**, max-length inputs)?  
- Does the system provide **clear error messages**?  
- Are **permission issues** addressed (if applicable)?  

 - Each story should have **at least one success scenario** and **one failure scenario** that help test the completeness and correctness of implementation.
  - Potential **unhappy paths** (failure scenarios) could including malformed inputs, missing fields, invalid data types, nonexistent resources, and permission issues
  - **Conditions** used for success or failure **must not be vague**, (ex. all valid, all invalid). It is important to be **specific** about what it means to be valid **to give a clear message to the user**. I call this the **Zob7lo2** Rule.
  - Imagine yourself **sketching theh interactions** with the user to think of good success and failure scenarios.
  - Think of **all the input** required from the user and is it account for. 
  - Do the scenarios mention the **result** of each interaction and **how it is displayed** to the user? 

##### **C. CRUD & Field Grouping**  
✅ Check:  
- Are **related fields** grouped into one story (e.g., "Create Project" with title, description)?  
- Are **standalone interactions** (e.g., file upload) split into separate stories?  
- Avoid "micro-stories" (e.g., "Enter Title" as a separate story).  

##### **D. Ambiguities & Gaps**  
✅ Flag:  
- Missing steps (e.g., no validation for a critical field).  
- Vague conditions (e.g., "valid input" without specifics).  
- Unrealistic flows (e.g., no error handling).  

#### **3. General Review**  
✅ Answer:  
- **Coverage**: Do all stories **collectively match the original requirements**?  
- **Epics**: Are any stories too large (need splitting)?  
- **Tiny Stories**: Are any stories just validations (need merging)?  



## Output format

Provide a list of notes per story about **what** needs to be changed and **why**?

#### **4. Output Format**  
✅ Structure feedback as:  

```json
[
  {
    "id": "US-001",
    "review_notes": ["What needs to be changed and why?"]
  }
]
```

#### **5. Final Checks**  
✅ Ensure:  
- **Functional focus**: No non-functional requirements (e.g., performance).  
- **Testability**: Scenarios are concrete enough for manual testing.  
- **User-centric**: Flows reflect real user behavior.  



