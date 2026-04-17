# Developer Journal – Task Manager Project

## Date
- April 17, 2026

## Feature Explored
- Task status update via CLI

## Main Components
- `cli.py` for command-line interface
- `task_manager.py` for core logic
- `storage.py` for persistence layer

## Executive Flow
- User runs CLI command
- CLI parses arguments and forwards to task manager
- Task manager updates task status
- Storage layer persists changes

### CLI Example
```bash
python cli.py update-status <task_id> in_progress
