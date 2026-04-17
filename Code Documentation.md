Task Manager Codebase – Documentation Exercise

Original Code (from task_manager.py)

def add_task(task_list, description, priority="medium"):
    task = {
        "description": description,
        "priority": priority,
        "status": "pending"
    }
    task_list.append(task)
    return task_list

Explanation:
- This function creates a new task as a dictionary with three fields: description, priority, and status.
- The status is always set to "pending" when a task is first created.
- The new task is appended to the existing list of tasks, and the updated list is returned.
- It is a simple but important function because it defines how tasks are introduced into the system.


Documentation Generated Using Prompt 1 (Comprehensive)

"""
add_task(task_list, description, priority="medium")

Adds a new task to the given task list.

Parameters:
- task_list (list): The current list of tasks.
- description (str): A short description of the task.
- priority (str, optional): The priority level of the task. 
  Accepts "low", "medium", or "high". Defaults to "medium".

Returns:
- list: The updated task list with the new task included.

Example:
>>> tasks = []
>>> add_task(tasks, "Finish homework", "high")
[{'description': 'Finish homework', 'priority': 'high', 'status': 'pending'}]
"""

Explanation:
- Prompt 1 focuses on technical completeness: listing parameters, return values, and examples.
- It ensures that anyone reading the documentation knows exactly how to call the function and what to expect.



Documentation Generated Using Prompt 1 (Comprehensive)

"""
add_task(task_list, description, priority="medium")

Adds a new task to the given task list.

Parameters:
- task_list (list): The current list of tasks.
- description (str): A short description of the task.
- priority (str, optional): The priority level of the task. 
  Accepts "low", "medium", or "high". Defaults to "medium".

Returns:


- list: The updated task list with the new task included.

Example:
>>> tasks = []
>>> add_task(tasks, "Finish homework", "high")
[{'description': 'Finish homework', 'priority': 'high', 'status': 'pending'}]
"""


Insights / Improvements Identified Using Prompt 2 (Intent & Logic)

- Intent: The function creates a new task with default status "pending" and adds it to the list.
- Logic: Build a dictionary, append it, return the updated list.
- Improvement: Validate the `priority` input to avoid invalid values.
- Improvement: Add a `due_date` or `created_at` field for better tracking.
- Insight: Inline comments could explain why "status" is set to "pending" by


Reflection on Documentation Exercise

Full Reflection – Documentation Exercise

Which part of the documentation was most challenging for the AI?
- The most difficult part for the AI was explaining the *intent and logic* of the function in a way that felt clear to a beginner. 
- Prompt 1 could easily generate technical details like parameters, return values, and examples, but it struggled to capture the “why” behind the code. 
- For example, it described what the function does but not why the status is set to "pending" or how priority values affect later behavior. 
- This showed me that AI is strong at structured technical writing but needs guidance to explain reasoning and business rules.

What additional information did I need to provide in my prompts?
- I had to give the AI more context about the project: that this was part of a Task Manager application. Without that, the documentation was too generic.  
- I needed to specify the type of documentation I wanted (comprehensive vs. intent/logic).  
- I had to provide examples of inputs and outputs so the AI could generate accurate docstrings.  
- I also had to ask it to highlight assumptions and edge cases, otherwise those details were missing.  
- In short, the more specific I was in my prompts, the better the documentation became.

How would I use this approach in my own projects?
- I would start by writing a simple draft of the documentation myself, then use AI prompts to expand it with more detail.  
- I would combine Prompt 1 (technical completeness) and Prompt 2 (intent and logic) to create final documentation that is both accurate and easy to understand.  
- This approach helps me learn the code better while also producing documentation that future developers can rely on.  
- In my own projects, I would use this method to document every new function I write, so my codebase stays clear and maintainable.  
- Over time, this will also make testing and debugging easier, because the documentation will already explain expected behavior and edge cases.

Conclusion
- The exercise taught me that documentation is not just about listing parameters, but about explaining the purpose and reasoning behind the code.  
- AI can generate strong drafts, but it needs context and guidance to produce documentation that is truly useful.  
- By combining my own understanding with AI prompts, I can create documentation that is both technically correct and beginner‑friendly.  
- This approach will help me grow as a software engineer and make my projects easier for others to understand and contribute to.

