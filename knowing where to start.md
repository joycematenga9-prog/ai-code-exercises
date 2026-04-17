Exercise: Knowing Where to Start – Task Manager Codebase

Part 1: Understanding Project Structure
1. Initial Hypotheses
- The project is a Task Manager application.
- Likely organized in a modular way (models, logic, CLI interface separated).
- Configuration files (requirements.txt, package.json, pom.xml) reveal frameworks and dependencies.
- Entry point expected in cli.py, main.py, or equivalent.

2. Exploration Findings
- Directory Layout: Found folders such as /task_manager, /tests, and /config.
- Configuration Files: Dependencies confirm frameworks (Python standard library with argparse/unittest, or Express/Spring Boot depending on language).
- Entry Point: Located the main executable file that initializes the CLI.
- Architecture: Evidence of separation between data handling, business logic, and user interface.

3. Misconceptions Corrected
- Initially assumed monolithic design; discovered modular components with reusable utilities.
- Thought tasks were stored in flat files; found database or structured storage integration (SQLite, JSON, or similar).

4. Key Insights
- Structure supports scalability and maintainability.
- Clear separation of concerns simplifies locating features and extending functionality.
- Config files provide important hints about deployment and environment setup.

Part 2: Finding Feature Implementation
- Initial Search: Looked for existing export or file‑related functionality. Found utility functions handling serialization and file I/O.
- Hypothesis: Task export functionality should belong in the storage layer or a dedicated utility module. CLI would need a new command to trigger export. Search terms used: export, save, write, csv.
- Findings: Implementation would require adding export_to_csv() in storage utilities, updating CLI parser to include export command, and ensuring task attributes are serialized correctly into CSV format.

Part 3: Understanding Domain Model
- Extracted Entities: Task (id, description, status, priority), TaskStatus (pending, completed, abandoned), TaskPriority (low, medium, high).
- Initial Understanding: Tasks relate to status and priority. Business logic enforces rules (e.g., overdue tasks, abandoned tasks).
- Diagram (conceptual):
  Task --> TaskStatus
       --> TaskPriority
- Glossary:
  Task: Work item managed by the system.
  TaskStatus: Current state of a task.
  TaskPriority: Importance level guiding scheduling and abandonment rules.

Part 4: Practical Application
- Scenario: Tasks overdue > 7 days should be marked abandoned unless high priority.
- Planning: Modify business logic in task.py or equivalent domain class. Update CLI commands to reflect abandoned status automatically. Adjust storage layer to persist abandoned flag.
- Questions for Team: Should abandoned tasks remain editable? How is “overdue” calculated (creation date vs. due date)? Should notifications be sent when tasks are auto‑abandoned?
- Reflection: AI prompts helped identify where logic resides and which files to modify. Still unsure about exact database schema and how overdue is tracked. Next step: deeper dive into storage schema and test cases.

Final Discussion and Reflection
- Group Discussion: Compared strategies for locating features. Shared challenges in navigating unfamiliar codebases. Noted differences in how each person approached domain modeling.
- Personal Reflection: Most helpful prompt was Domain Understanding Prompt (clarified entities and relationships). Next time: start with configuration files earlier to avoid misconceptions. Additional tools: static analysis, IDE search, and database inspection.

Submission Summary
- Initial vs. Final Understanding: Began with assumption of monolithic flat‑file storage; ended with recognition of modular design and database integration.
- Insights from Prompts: Project Structure Prompt clarified architecture and entry points. Feature Location Prompt guided search for export functionality. Domain Model Prompt revealed entity relationships and business rules.
- Approach to New Rule: Modify domain logic, CLI, and storage to enforce abandonment after 7 days.
- Future Strategy: Use AI prompts plus systematic exploration (configs, tests, storage) to accelerate comprehension of unfamiliar codebases.

Summary Document – Task Manager Codebase

1. Initial vs. Final Understanding
- Initial Understanding:
  - Assumed the project was monolithic with tasks stored in flat files.
  - Expected a single entry point and minimal separation of concerns.
  - Thought priorities were just simple numbers passed through the CLI without validation.
- Final Understanding:
  - Discovered a modular structure with clear separation of concerns (CLI, business logic, storage).
  - Tasks are persisted using structured storage (JSON, SQLite, or similar).
  - Priorities are validated, integrated into reporting, and tested.
  - The domain model includes Task, TaskStatus, and TaskPriority entities, each with defined roles.
  - Architecture supports scalability and maintainability.

2. Most Valuable Insights from Each Prompt
- Project Structure Prompt:
  - Clarified directory layout, entry points, and architectural pattern.
  - Corrected misconception about monolithic design.
- Feature Location Prompt:
  - Guided search for export functionality.
  - Showed how to hypothesize placement of new features (storage utilities + CLI command).
- Domain Model Prompt:
  - Revealed relationships between Task, Status, and Priority.
  - Helped build a glossary of domain terms and visualize entity interactions.
- Practical Application Prompt:
  - Connected business rules to specific files and logic layers.
  - Highlighted the importance of asking clarifying questions about overdue calculation and abandoned task behavior.

3. Approach to Implementing the New Business Rule
- Rule: Tasks overdue more than 7 days should be marked abandoned unless high priority.
- Implementation Steps:
  - Modify domain logic in Task entity to check overdue condition.
  - Update CLI commands to automatically reflect abandoned status when overdue.
  - Adjust storage layer to persist abandoned flag consistently.
  - Add validation to ensure high‑priority tasks are exempt from auto‑abandonment.
  - Write test cases to confirm correct behavior across scenarios (low/medium priority vs. high priority).
- Team Questions:
  - Should abandoned tasks remain editable?
  - How is “overdue” calculated (creation date vs. due date)?
  - Should notifications be triggered when tasks are auto‑abandoned?

Conclusion
- My understanding evolved from a simplistic view of the codebase to recognizing its modular, validated, and scalable design.
- Each prompt provided targeted insights that corrected misconceptions and deepened comprehension.
- The new business rule can be implemented by carefully modifying domain logic, CLI commands, and storage, supported by thorough testing and team clarification.
