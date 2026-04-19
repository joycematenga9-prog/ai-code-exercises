Exercise: Function Decomposition Challenge  
Chosen Function: calculate_task_score (Python)

Step 1 – Identify Distinct Responsibilities  
The original function mixes several responsibilities:  
- Checking task priority (LOW, MEDIUM, HIGH)  
- Adjusting score for overdue or due‑soon tasks  
- Reducing score if status is DONE  
- Adding points for tags like "urgent" or "important"  
- Adjusting score based on last update time  

Step 2 – Create a Decomposition Plan  
Break the function into smaller helpers, each with a single clear purpose:  
- score_priority(priority)  
- score_due_date(due_date)  
- score_status(status)  
- score_tags(tags)  
- score_update_time(last_updated)  

Step 3 – Extract Helper Functions  
Each helper returns an integer adjustment.  
Examples:  
- score_priority: HIGH = +30, MEDIUM = +20, LOW = +10  
- score_due_date: overdue = +35, due today = +10, future = 0  
- score_status: DONE = −50, else 0  
- score_tags: "urgent" = +20, "important" = +15  
- score_update_time: recent update = +5, stale update = −5  

Step 4 – Refactor Main Function  
The main function becomes an orchestrator:  
- Initialize score = 0  
- Add contributions from each helper  
- Return final score  

Step 5 – Run Tests to Verify Behavior  
Unit tests for each helper:  
- HIGH priority returns +30  
- Overdue due_date returns +35  
- DONE status returns −50  
Integration test for calculate_task_score:  
- Task with HIGH priority, overdue, urgent tag → score reflects all rules combined  
- Task with LOW priority, no due date, DONE status → score reflects reductions  

Step 6 – Document Refactoring Approach and Benefits  
Benefits gained:  
- Readability: each scoring rule is isolated and easy to follow  
- Maintainability: changes to one rule don’t affect others  
- Reusability: helpers like score_due_date can be reused in other contexts  
- Testability: unit tests can target specific scoring logic without running the whole function  

Reflection  
Breaking down the function improved readability by reducing nested conditionals and clarifying responsibilities. 
The most challenging part was deciding how to group related rules, such as due date versus update time.
The most reusable extracted function is score_due_date, since due‑date logic is common across many task management features.