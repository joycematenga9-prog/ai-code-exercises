Exercise 1.1 – Behaviour Analysis

1. Empty task list  
   Input: []  
   Expected Result: Program should handle gracefully and print nothing, without raising IndexError.

2. Single task in the list  
   Input: [Task("Buy milk", "Pending")]  
   Expected Result: Program should print the single task correctly, with no errors.

3. Multiple tasks in the list  
   Input: [Task("Buy milk", "Pending"), Task("Do homework", "Completed")]  
   Expected Result: Program should print both tasks correctly with proper numbering.

4. Edge Case – Off‑by‑one loop error  
   Input: [Task("Task1", "Pending"), Task("Task2", "Pending")]  
   Expected Result: If the loop uses `range(len(tasks) + 1)`, this test will trigger IndexError when trying to access a non‑existent third index.

5. Edge Case – Large task list  
   Input: 1,000 tasks generated in a loop  
   Expected Result: Program should print all tasks without crashing or slowing down significantly.

6. Edge Case – Invalid index access (manual test)  
   Input: Attempt to access tasks[10] when only 5 tasks exist  
   Expected Result: Program should raise IndexError, confirming the importance of boundary checks.

   Exercise 1.2 – Test Planning Document

Goal:  
To design a comprehensive test plan for the task prioritization functions (`calculate_task_score`, `sort_tasks_by_importance`, `get_top_priority_tasks`) based on the conversation with AI. The plan ensures correctness, handles edge cases, and validates integration between functions.

---

Functions Under Test:
- calculate_task_score(task): Computes a numeric score based on priority, due date, status, tags, and update time.
- sort_tasks_by_importance(tasks): Sorts tasks by their calculated score, highest first.
- get_top_priority_tasks(tasks, limit): Returns the top N tasks by importance.




Part 2 – Exercise 2.1  
Structured Test Plan Document

Goal:  
To verify correctness and robustness of the task prioritization functions (`calculate_task_score`, `sort_tasks_by_importance`, `get_top_priority_tasks`) using unit and integration tests. The plan includes test case priorities, types of tests, dependencies, and expected outcomes.

Functions Under Test:
- calculate_task_score(task): Computes a numeric score based on priority, due date, status, tags, and update time.
- sort_tasks_by_importance(tasks): Sorts tasks by their calculated score, highest first.
- get_top_priority_tasks(tasks, limit): Returns the top N tasks by importance.


1. Basic Priority Weights
   - Priority: High  
   - Type: Unit test (calculate_task_score)  
   - Dependencies: TaskPriority enum values must be defined.  
   - Expected Outcome: A HIGH priority task scores higher than MEDIUM or LOW tasks with no other factors.

2. Due Date Factor – Overdue Task
   - Priority: High  
   - Type: Unit test (calculate_task_score)  
   - Dependencies: datetime.now() must be available.  
   - Expected Outcome: Overdue tasks receive +35 points, ranking above non‑overdue tasks of equal priority.

3. Status Reduction – Completed Task
   - Priority: Medium  
   - Type: Unit test (calculate_task_score)  
   - Dependencies: TaskStatus enum values must be defined.  
   - Expected Outcome: DONE tasks reduce score by 50, ensuring they fall to the bottom of sorted results.

4. Tag Boost – Critical Task
   - Priority: Medium  
   - Type: Unit test (calculate_task_score)  
   - Dependencies: Task must contain tags list.  
   - Expected Outcome: Tasks tagged “critical” or “urgent” gain +8 points, boosting them above similar tasks without tags.

5. Recently Updated Task
   - Priority: Medium  
   - Type: Unit test (calculate_task_score)  
   - Dependencies: updated_at timestamp must be set.  
   - Expected Outcome: Tasks updated within the last day gain +5 points.

6. Integration – Sorting Order 
   - Priority: High  
   - Type: Integration test (sort_tasks_by_importance)  
   - Dependencies: calculate_task_score must be correct.  
   - Expected Outcome: Tasks are sorted in descending order of score, with ties resolved consistently.

7. Integration – Top N Tasks
   - Priority: High  
   - Type: Integration test (get_top_priority_tasks)  
   - Dependencies: sort_tasks_by_importance must work correctly.  
   - Expected Outcome: Function returns exactly N tasks, highest scoring first.

8. Edge Case – Empty Task List
   - Priority: High  
   - Type: Unit + Integration  
   - Dependencies: None.  
   - Expected Outcome: Functions return empty lists without error.

9. Edge Case – Large Task List (Performance)
   - Priority: Low (performance validation)  
   - Type: Integration test  
   - Dependencies: Efficient sorting implementation.  
   - Expected Outcome: Functions handle thousands of tasks within acceptable runtime.

10. Edge Case – Invalid Data 
    - Priority: Medium  
    - Type: Unit test  
    - Dependencies: Input validation.  
    - Expected Outcome: Tasks missing required fields (priority, status) should not crash; either default values or handled error

Part 2 – Exercise 2.2  
Comprehensive Test Plan for Due Date Calculation

Goal:  
To verify that the due date factor in `calculate_task_score` correctly adjusts task scores based on whether tasks are overdue, due soon, or not due at all.

Functionality Under Test:
- `calculate_task_score(task)` → adds +35 points if task is overdue (due date < today), adjusts score for tasks due soon, and leaves score unchanged for tasks with no due date.

Part 2 – Exercise 2.2  
Comprehensive Test Plan for Due Date Calculation

Goal:  
To verify that the due date factor in calculate_task_score correctly adjusts task scores depending on whether tasks are overdue, due today, due soon, or have no due date.

Functions Under Test:  
- calculate_task_score(task): Adds +35 points if overdue, smaller boost if due today, no change if future or no due date.

Test Cases:

1. Overdue Task  
   Priority: High  
   Type: Unit test  
   Dependencies: Task must have a valid due_date earlier than current datetime.  
   Expected Outcome: Score increases by +35 points, ensuring overdue tasks rank above non‑overdue tasks.

2. Task Due Today  
   Priority: High  
   Type: Unit test  
   Dependencies: Task due_date equals current date.  
   Expected Outcome: Task receives urgency boost (e.g., +10 points), reflecting immediate deadline.

3. Task Due Tomorrow  
   Priority: Medium  
   Type: Unit test  
   Dependencies: Task due_date is one day after current date.  
   Expected Outcome: Task is not overdue; score remains unchanged unless rules specify a “due soon” boost.

4. Task with No Due Date  
   Priority: Medium  
   Type: Unit test  
   Dependencies: Task object must allow due_date=None.  
   Expected Outcome: No due‑date points applied; score depends only on other factors (priority, status, tags, update time).

5. Integration – Mixed Due Dates  
   Priority: High  
   Type: Integration test (sort_tasks_by_importance)  
   Dependencies: calculate_task_score must apply due date logic correctly.  
   Expected Outcome: Overdue tasks appear at the top of the sorted list, followed by tasks due today, then tasks with future or no due dates.

6. Edge Case – Large Task List  
   Priority: Low (performance validation)  
   Type: Integration test  
   Dependencies: Efficient sorting implementation.  
   Expected Outcome: Sorting thousands of tasks with varied due dates completes within acceptable runtime, with overdue tasks consistently ranked highest.

Part 3 – Exercise 3  
Test‑Driven Development (TDD) Plan for New Feature

New Feature:  
Add a function get_tasks_due_within(days) that returns all tasks with a due date within the next N days.

TDD Approach:  
1. Write failing tests first to define expected behavior.  
2. Implement minimal code to make tests pass.  
3. Refactor code while keeping tests green.  
4. Extend tests to cover edge cases and integration scenarios.

Test Cases (with priority, type, dependencies, expected outcomes):

1. No Tasks in List  
   Priority: High  
   Type: Unit test  
   Dependencies: Task list must be empty.  
   Expected Outcome: Function returns an empty list without error.

2. Tasks Due Within Range  
   Priority: High  
   Type: Unit test  
   Dependencies: Task due_date set to today + 2 days, with days=3.  
   Expected Outcome: Task is included in the result list.

3. Tasks Outside Range  
   Priority: High  
   Type: Unit test  
   Dependencies: Task due_date set to today + 5 days, with days=3.  
   Expected Outcome: Task is excluded from the result list.

4. Mixed Task List  
   Priority: High  
   Type: Integration test  
   Dependencies: calculate_task_score must still work correctly.  
   Expected Outcome: Only tasks due within N days are returned, sorted by importance if combined with sort_tasks_by_importance.

5. Edge Case – Task Due Today  
   Priority: High  
   Type: Unit test  
   Dependencies: Task due_date equals current date.  
   Expected Outcome: Task is included in the result list.

6. Edge Case – Task with No Due Date  
   Priority: Medium  
   Type: Unit test  
   Dependencies: Task object must allow due_date=None.  
   Expected Outcome: Task is excluded from the result list.

7. Large Task List Performance  
   Priority: Low  
   Type: Integration test  
   Dependencies: Efficient filtering implementation.  
   Expected Outcome: Function handles thousands of tasks within acceptable runtime.

Part 3 – Exercise 3.2  
TDD Plan for Bug Fix

Bug Description:  
The original code in cli.py used range(len(tasks) + 1), which caused an IndexError when the loop attempted to access a non‑existent index.  

Fix Goal:  
Correct the loop boundary so that tasks are iterated safely without exceeding the list length.

TDD Approach:  
1. Write failing tests that reproduce the bug.  
2. Implement the minimal fix (remove +1).  
3. Run tests to confirm the fix.  
4. Add edge case tests to ensure robustness.  
5. Refactor if needed while keeping tests green.


Test Cases (with priority, type, dependencies, expected outcomes):

1. Empty Task List  
   Priority: High  
   Type: Unit test  
   Dependencies: Task list must be empty.  
   Expected Outcome: Loop runs zero times, no IndexError raised.

2. Single Task  
   Priority: High  
   Type: Unit test  
   Dependencies: Task list contains one task.  
   Expected Outcome: Task is printed once, no IndexError.

3. Two Tasks (Boundary Check)  
   Priority: High  
   Type: Unit test  
   Dependencies: Task list contains two tasks.  
   Expected Outcome: Both tasks printed correctly, loop does not attempt a third index.

4. Bug Reproduction (Original Code)  
   Priority: High  
   Type: Unit test  
   Dependencies: Original buggy oop with range(len(tasks) + 1).  
   Expected Outcome: IndexError raised when accessing tasks[2] in a two‑task list.

5. Large Task List  
   Priority: Medium  
   Type: Integration test  
   Dependencies: Efficient iteration.  
   Expected Outcome: All tasks printed correctly, no IndexError, acceptable performance.



First Failing Test (pytest style):


import pytest

class Task:
    def __init__(self, title):
        self.title = title

# Original buggy function (for demonstration)
def print_tasks_buggy(tasks):
    for i in range(len(tasks) + 1):  # Bug: +1 causes IndexError
        print(tasks[i].title)

def test_bug_reproduction():
    tasks = [Task("Task1"), Task("Task2")]
    with pytest.raises(IndexError):
        print_tasks_buggy(tasks)


 Part 4 – Exercise 4.1  
Integration Test for Full Workflow

Goal:  
To validate that the workflow of calculating task scores, sorting tasks by importance, and retrieving the top priority tasks with correct and consistent results.

Functions Under Test:  
- calculateTaskScore(task): Computes a numeric score based on priority, due date, status, tags, and update time.  
- sortTasksByImportance(tasks): Sorts tasks in descending order of score.  
- getTopPriorityTasks(tasks, limit): Returns the top N tasks by importance.

---

Integration Test Scenarios:

1. Mixed Priority and Due Dates  
   Priority: High  
   Type: Integration test  
   Dependencies: All three functions must be implemented correctly.  
   Expected Outcome:  
   - High priority overdue tasks appear first.  
   - Medium priority tasks follow.  
   - Completed tasks rank lowest.

2. Top N Selection  
   Priority: High  
   Type: Integration test  
   Dependencies: sortTasksByImportance must produce correct ordering.  
   Expected Outcome:  
   - getTopPriorityTasks returns exactly N tasks.  
   - Tasks are the highest scoring ones from the sorted list.

3. Edge Case – Empty Task List  
   Priority: High  
   Type: Integration test  
   Dependencies: None.  
   Expected Outcome:  
   - All functions return empty lists without error.

4. Edge Case – Tasks with No Due Date  
   Priority: Medium  
   Type: Integration test  
   Dependencies: calculateTaskScore must handle None values.  
   Expected Outcome:  
   - Tasks without due dates are scored only on priority, status, tags, and update time.  
   - Sorting and top‑N selection remain consistent.

5. Large Task List Performance  
   Priority: Low  
   Type: Integration test  
   Dependencies: Efficient sorting implementation.  
   Expected Outcome:  
   - Workflow handles thousands of tasks within acceptable runtime.  
   - Results remain correct and consistent.

---

Example Integration Test (pytest style):

```python
import datetime

class Task:
    def __init__(self, title, priority, due_date=None, status="PENDING"):
        self.title = title
        self.priority = priority
        self.due_date = due_date
        self.status = status

def test_full_workflow():
    today = datetime.date.today()
    tasks = [
        Task("Overdue High", priority="HIGH", due_date=today - datetime.timedelta(days=1)),
        Task("Future Medium", priority="MEDIUM", due_date=today + datetime.timedelta(days=5)),
        Task("Completed Low", priority="LOW", due_date=today, status="DONE"),
    ]

    # Step 1: Calculate scores
    scored_tasks = [(t, calculateTaskScore(t)) for t in tasks]

    # Step 2: Sort by importance
    sorted_tasks = sortTasksByImportance(tasks)

    # Step 3: Get top N tasks
    top_tasks = getTopPriorityTasks(sorted_tasks, 2)

    # Assertions
    assert sorted_tasks[0].title == "Overdue High"
    assert "Completed Low" in [t.title for t in sorted_tasks]
    assert len(top_tasks) == 2
    assert top_tasks[0].title == "Overdue High"

reflection

Through this exercise I learned how testing evolves from unit checks to full workflow validation. I saw that integration testing is essential because even correct individual functions can fail when combined. Edge cases like empty lists or overdue tasks taught me to anticipate unusual inputs. Applying TDD gave me confidence in bug fixes and new features, while AI support helped me identify dependencies and prioritize tests more effectively.