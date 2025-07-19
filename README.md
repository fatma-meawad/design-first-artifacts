# Design-First Workflow Artifacts

This repository contains all artifacts used in “Orchestrating LLM-Based Software Generation: A Design-First, Contract-Driven Workflow”. 

### **Repository Overview**
This repository (`design-first-artifacts/design-first-workflow`) contains example artifacts, prompts, roles, and JSON-based repository objects demonstrating the output of our experiments. 

---

### **Key Directories & Files**
1. **`generated_artifacts/`**  
   - Contains output files JSON files with intermediate artifacts that are generated throughout the workflow execution: wireframes, API specifications, development plan or user stories.  

2. **`hbs_templates/`**  
   - Handlebars (`.hbs`) templates used to dynamically generate artifacts clean architecture out of the openapi specifications.

3. **`repo_objects/`**  
   - JSON files representing code bases generated out of the three different strategies.
     
4. **`roles/`**  
   - Define System prompts for different roles
     
5. **`tasks/`**  
   - Structured task prompts and function steps for different tasks in the workflow.

