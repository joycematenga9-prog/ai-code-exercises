# understanding Journal - Task Manager project
Date: 17 CodeApril 2026

#Feature Explored
Updating tasks and managing tags

#Main components
cli.py : runs commands like update-status, update-due-date, add tag, remove tag
Core logic: applies changes to task and saves them
Storage : keeps updated task info
ffrrrrrrrrrrrrrrrrrrrrr
#Execution flow 
Run a command:
python cli.py update-status <task_id> in_progress
CLI parses input 
Task is updated in Storage
confirmation or updated output is shown

#Data Storage
same storage layer as task creation (likely JSON or SQLite)
Tags and status changes are saved for later retrieval

#Design Patterns Observed
**Command Pattern**
Each CLI command (create, list, update, add_tag, remove-tag)acts like a command object that triggers a specific action.

**Separation of Concerns**
cli.py handles input parsing, core logic manages tasks, and storage layer persists data.

**MVC-like Structures**
- Model = Task object
- Controller = CLI commands 
- View = Printed output in the terminal

**Builder Pattern(possible)**
- Task Creation builds a new Task object step by step with parameters like title, description , priority, and due date

# Developer Journal: Task Manager Project – Task Prioritization System

## Initial Understanding
- The task manager project needed a way to handle priorities for tasks.
- At first glance, priorities seemed like a simple attribute, but their integration across the system required deeper exploration.
- I assumed priorities were just labels without much validation or impact beyond display.

## Guided Questions & Discoveries
- **Where is priority defined?**
  - Priority is defined as a field in the `Task` object.
- **How is priority updated?**
  - It is updated through commands in `cli.py`.
- **Is priority validated?**
  - Yes, the system validates that only allowed values (e.g., low, medium, high) can be set.
- 

## Key Insights
- Priorities are **validated** to ensure consistency and prevent invalid entries.
- They are **integrated into reporting**, making stats more meaningful by showing not just status but also priority breakdowns.
- The prioritization system is **covered by tests**, ensuring reliability and catching regressions early.

## Misconceptions Clarified
- Initially, I thought there was **no validation** for priority values — but validation is indeed enforced.
- I also believed that **stats only used task status** (e.g., completed vs. pending), but they actually incorporate priority as well, enriching the reporting system.
EXERCISE 3
## Data flow - marking task complete

```c#
+----------------+
|   CLI Command  |
+----------------+
        |
        v
+---------------------------+
| core logic: update-status |
|        function           |
+---------------------------+
        |
        v
+--------------------------------+
| Task object: status field      |
| updated to "completed"         |
+--------------------------------+
        |
        v
+--------------------------------------+
| Storage layer: JSON / SQLite         |
| persistence of updated task status   |
+--------------------------------------+
        |
        v
+--------------------------------------+
| Reporting / Stats: task now shown    |
| as completed in summaries/analytics  |
+--------------------------------------+

## Task completion - state changes and persistence

### 1. State changes
- The **Task object’s status field** changes from *in progress* to *completed*.
- The **storage layer** (JSON file or SQLite database) is updated with the new status.
- **Reporting features** (e.g., stats, summaries, task lists) reflect the updated status, showing the task as completed.

### 2. Potential points of failure
- **Invalid task_id**: update fails because the task cannot be found.
- **Storage write errors**: persistence fails if the JSON file or SQLite database cannot be written to.
- **CLI parsing errors**: incorrect or malformed arguments prevent the command from executing properly.

### 3. How the application persists these changes
- The updated status is saved in the **same storage layer** used during task creation (JSON or SQLite).
- Subsequent commands such as **list** or **stats** query the storage layer and display the task as *completed*.
- This ensures consistency between the **task object in memory**, the **persistent storage**, and the **reporting layer**.

## Exercise 4: Reflection and Presentation (3–5 minutes)

### Reflection
- When I first approached the unfamiliar codebase, I felt uncertain about where to begin.  
- Using AI prompts helped me scaffold my exploration: I mapped the project structure, located relevant features, and clarified the domain model.  
- My understanding evolved from vague impressions to a clearer picture of how tasks, persistence, and reporting interact.  
- I still recognize gaps, such as edge cases and deeper business rules, but I now know where to look and how to ask better questions.  

### Presentation
- In our group discussion, I’ll highlight how prompts accelerated comprehension compared to manual exploration.  
- I’ll share that the **Domain Understanding prompt** was most valuable, since it clarified entities like `Task`, `TaskStatus`, and `TaskPriority`.  
- I’ll also note that visual aids (like diagrams) would have helped earlier, and that combining AI prompts with IDE navigation and static analysis tools is a strong strategy.  
- For future unfamiliar codebases, I’ll emphasize documenting misconceptions, testing features hands-on, and pairing with teammates to validate assumptions.  

### Closing
- Overall, the exercise showed me that structured prompting is not just about answers—it’s about building confidence and a roadmap through complexity.  
- My key takeaway: AI prompts are a powerful complement to traditional exploration, but persistence and collaboration remain essential.  
