Task Manager Project – Documentation Exercise

1. Project Selected
I chose the Task Manager project from the WTC AI exercises. This project manages tasks with attributes like description, priority, and status, and includes functions to add, complete, and list tasks.

2. Prompt 1 – Comprehensive README File

# Task Manager

Overview
The Task Manager project is a simple application for creating, managing, and tracking tasks. Each task has a description, priority level, and status. The project demonstrates modular design, separation of concerns, and basic persistence.

Features
- Add new tasks with description and priority.
- Mark tasks as complete.
- List all tasks with their current status.
- Extendable design for adding new rules (e.g., overdue tasks).

Installation
1. Clone the repository:
   git clone https://github.com/wethinkcode/ai-code-exercises
2. Navigate to the project folder:
   cd use-code-algorithms/task_manager
3. Run the CLI:
   python cli.py

Usage
- Add a task: add_task(tasks, "Finish homework", "high")
- Complete a task: complete_task(tasks, 0)
- List tasks: list_tasks(tasks)

Requirements
- Python 3.8+
- Basic knowledge of lists and dictionaries

License
This project is for educational use in the WTC AI curriculum.

3. Review of README File
- The README is complete and covers overview, features, installation, usage, and requirements.
- Improvement: Add screenshots or sample outputs for clarity.
- Improvement: Include testing instructions (e.g., how to run pytest).

4. Prompt 2 – Step-by-Step Guide for a Feature

Step-by-Step Guide: Adding a Task
1. Open the CLI by running python cli.py.
2. Choose the option to add a task.
3. Enter the task description (e.g., "Finish homework").
4. Select the priority level ("low", "medium", "high").
5. The system will create a new task with status "pending".
6. The task is added to the list and saved.

This guide helps beginners understand exactly how to use the add_task feature.

5. Prompt 3 – FAQ Document

FAQ – Task Manager Project

Q: What happens if I don’t specify a priority?  
A: The system defaults to "medium" priority.

Q: Can I edit a task after creating it?  
A: Currently, tasks can only be marked complete. Editing descriptions or priorities would require extending the code.

Q: How are tasks stored?  
A: Tasks are stored in memory as dictionaries inside a list. Persistence can be added later.

Q: What is the default status of a new task?  
A: Every new task starts with status "pending".

Q: How do I run tests?  
A: Navigate to the tests folder and run pytest.

6. Feedback
- Prompt 1 was strong at generating a structured README, but I had to review it for completeness and add missing details like testing instructions.  
- Prompt 2 helped me create a clear step-by-step guide, which is useful for beginners.  
- Prompt 3 produced a helpful FAQ, but I needed to think about common beginner questions myself.  
- Overall, combining all three prompts gave me a comprehensive set of documentation: technical overview, user guide, and FAQ. This approach makes the project easier to understand and maintain.
 