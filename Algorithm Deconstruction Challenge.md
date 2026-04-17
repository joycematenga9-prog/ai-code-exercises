from datetime import datetime, timedelta
from enum import Enum

# --- Enums for clarity ---
class TaskPriority(Enum):
    LOW = 1
    MEDIUM = 2
    HIGH = 3
    URGENT = 4

class TaskStatus(Enum):
    TODO = 1
    IN_PROGRESS = 2
    REVIEW = 3
    DONE = 4

# --- Task model ---
class Task:
    def __init__(self, title, priority, due_date, status, tags, updated_at):
        self.title = title
        self.priority = priority
        self.due_date = due_date
        self.status = status
        self.tags = tags
        self.updated_at = updated_at


        #  Documented Insights & Learning Points

#  Key Insights
1. *Algorithm Purpose* 
   - The function calculates a **priority score** for tasks.  
   - It combines multiple factors (priority, due date, status, tags, updates).  
   - The score is used to **rank tasks by importance** and select the top N.

2. *Core Technique*  
   - This is a **weighted scoring heuristic**.  
   - Each property nudges the score up or down.  
   - Commonly used in scheduling, ranking, and recommendation systems.

3. **Learning Point: Breaking Down Algorithms**  
   - Splitting the function into sections (priority, due date, status, tags, updates) makes it easier to understand.  
   - Flow diagrams help visualize the pipeline of adjustments.  
   - Walking through a concrete example clarifies how numbers change step by step.

---

# Flow Diagram

```text
Task Input
    │
    ▼
Priority → Base Score
    │
    ▼
Due Date → Adjust Score
    │
    ▼
Status → Adjust Score
    │
    ▼
Tags → Adjust Score
    │
    ▼
Recent Update → Adjust Score
    │
    ▼
Final Score → Sort → Top N Tasks


#  Reflection on Algorithm Deconstruction Challenge

# How did the AI's explanation change my understanding?
The AI’s explanation helped me see the algorithm as a **step-by-step scoring pipeline** rather than just a block of code. Breaking it into sections (priority, due date, status, tags, updates) made the logic clearer. The flow diagrams showed me how each factor nudges the score up or down, which I hadn’t noticed before. Walking through a concrete example also made the scoring process more tangible.

---

# What aspects were still difficult to understand?
Even after the explanation, I still found it tricky to fully grasp:
- **Why certain weights were chosen** (e.g., why overdue adds +35 instead of another number).
- **How negative scores behave** in sorting — I understand they drop tasks down the list, but I’m not sure if that’s always the best approach.
- **Balancing factors** — it’s not obvious how to decide the right balance between due dates, tags, and updates.

---

# How would I explain this algorithm to another junior developer?
I would say:  
“This algorithm gives each task a score based on its priority, deadline, status, tags, and how recently it was updated. Think of it like a checklist where each property adds or subtracts points. At the end, tasks are sorted by their total score, and the highest ones are considered the most important. It’s basically a **ranking system** that combines multiple signals into one number.”

---

# Did I test this understanding against AI?
Yes. I tested my understanding by asking the AI to walk through an example task. Seeing the score change step by step confirmed that I understood the pipeline correctly. The reflection questions also helped me check if I could apply the logic to edge cases (like overdue + done tasks).

---

# How might I improve the algorithm based on my understanding?
- **Adjust weights dynamically**: Instead of fixed numbers, make the weights configurable so teams can tune them to their workflow.  
- **Handle negative scores differently**: Maybe cap the minimum score at zero so completed tasks don’t go into negatives.  
- **Add more context factors**: For example, boost tasks assigned to multiple people or tasks linked to blockers.  
- **Use machine learning later**: Replace hard-coded weights with learned weights from past task completions.

---

## Beginner’s Takeaway
As a beginner, I learned that algorithms often use simple scoring heuristics to solve complex problems. Breaking them down into diagrams and examples makes them much easier to understand. I also realized that the numbers chosen in the algorithm are design decisions, not absolute truths — they can be improved or adapted.
