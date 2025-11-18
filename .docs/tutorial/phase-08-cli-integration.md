# Phase 8: Python CLI Integration with Copilot

[← Previous: Phase 7](./phase-07-enterprise-features.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 9 →](./phase-09-testing-refinement.md)

---

**Goal:** Use Copilot to build a Python CLI tool for managing board data and JSON files  
**Duration:** ~45 minutes  
**Focus:** Python-based backend data management through `board_manager.py`

### 8.1 Python CLI Architecture with Copilot
- Design Python CLI using `argparse` or `click`
- Build `board_manager.py` module with Copilot
- JSON file operations with Python's `json` module
- Copilot-assisted data validation and error handling

**🤖 Copilot Techniques:**
- **Module Design**: Copilot structures Python modules with proper organization
- **CLI Framework**: Copilot knows `argparse` and `click` patterns
- **File I/O Safety**: Copilot adds context managers and error handling
- **Type Hints**: Copilot adds Python type annotations for clarity

**Example Prompts:**
```
"Create a Python module board_manager.py with functions to interact with 
boards.json and task JSON files. Include functions for loading, validating, 
and saving board data with proper error handling."

"Generate a Python CLI using argparse that can add tasks, move tasks between 
columns, and list all tasks with filtering options."

"Write a Python function that reads a JSON file safely using context managers, 
validates the structure, and returns the data as a dictionary."
```

**📌 Key Copilot Learning Points:**
- **Pythonic patterns**: Copilot uses context managers (`with open()`) automatically
- **Type hints**: Copilot adds `-> dict`, `list[dict]` for better code clarity
- **Error handling**: Copilot includes `try/except` for JSON decode errors
- **Path handling**: Copilot uses `pathlib.Path` for cross-platform compatibility

**ID Generation Convention:**

**ID Formats:**
- Task IDs: `task-001`, `task-002`, `task-003`, etc.
- Activity IDs: `act-001`, `act-002`, etc.
- Epic IDs: `epic-001`, `epic-002`, etc.

**Prompt Copilot to generate Python ID function:**
- Comment: `# Generate next task ID in format task-XXX by finding max ID and incrementing`
- Start typing: `def generate_task_id(existing_tasks: list[dict]) -> str:`
- Copilot will suggest logic to:
  - Extract numbers from existing IDs using regex or string slicing
  - Find maximum ID number
  - Add 1
  - Format with zero-padding (3 digits) using f-string

**Or ask Copilot Chat:**
```
"Create a Python function that generates sequential task IDs in format task-001 
by finding the highest existing ID number and adding 1. Use type hints and 
return the formatted string."
```

**Timestamp Conventions:**

**Format: ISO 8601 (UTC timezone)**
- Example: `"2025-11-17T10:30:00.000Z"`

**Prompt Copilot for Python timestamps:**
- Comment: `# Generate current timestamp in ISO 8601 format`
- Copilot suggests: `from datetime import datetime, timezone` + `datetime.now(timezone.utc).isoformat()`

**For activity entries:**
- Comment: `# Create activity dict with current ISO timestamp`
- Copilot generates complete dictionary with proper timestamp field

**Ask Copilot Chat:**
```
"How do I generate ISO 8601 formatted timestamps in Python for activity log 
entries? Show me with the datetime module."
```

### 8.2 Building board_manager.py with Copilot
- Core functions for JSON file operations
- Task CRUD operations (Create, Read, Update, Delete)
- Data validation with Python
- Copilot-assisted modular design

**🤖 Copilot Techniques:**
- **Function Generation**: Copilot creates complete functions with docstrings
- **Error Handling**: Copilot adds `FileNotFoundError`, `JSONDecodeError` handling
- **Type Safety**: Copilot includes type hints and Optional types
- **Pathlib Usage**: Copilot uses modern `Path` objects instead of string paths

**Example Prompts:**
```
"Create a Python function load_board_data(board_name: str) -> dict that reads 
boards.json, finds the board by name, loads its tasks file, and returns the 
complete board data with tasks. Include error handling."

"Write a Python function add_task_to_board() that creates a new task dictionary 
with all required fields, generates an ID, adds an activity entry, appends to 
the tasks list, and saves the file atomically."

"Generate a function move_task_column() that updates a task's status, sets 
appropriate timestamps (startedAt, completedAt), adds an activity log entry, 
and saves the updated tasks."
```

**📌 Key Copilot Learning Points:**
- **Copilot writes working Python**: Generated code follows PEP 8 style
- **Imports included**: Copilot adds necessary imports (json, pathlib, datetime)
- **Docstrings automatic**: Copilot writes Google or NumPy style docstrings
- **Learn Python patterns**: Study Copilot's use of comprehensions, context managers

**🤖 Copilot Workflow for board_manager.py:**

**Step 1: Write module docstring**
```python
"""
board_manager.py - Backend data management for ProjectBoard

Provides functions to interact with boards.json and task JSON files.
Handles all file I/O, validation, and data integrity for the Kanban board system.
"""
```

**Step 2: Copilot suggests imports**
```python
# Import modules for file operations, JSON handling, and timestamp generation
```
Copilot adds:
```python
import json
from pathlib import Path
from datetime import datetime, timezone
from typing import Optional
```

**Step 3: Write function signature with docstring**
```python
def load_json_file(file_path: Path) -> dict:
    """Load and parse a JSON file safely.
    
    Args:
        file_path: Path to the JSON file
        
    Returns:
        Parsed JSON data as dictionary
        
    Raises:
        FileNotFoundError: If file doesn't exist
        JSONDecodeError: If file contains invalid JSON
    """
```

**Step 4: Copilot implements complete logic** including context managers and error handling

### 8.3 Data Validation with Python and Copilot
- Generate validation functions with Copilot
- Use Python dataclasses or Pydantic for structure
- Comprehensive data integrity checks
- Copilot-assisted error messaging

**🤖 Copilot Techniques:**
- **Validation Generators**: Copilot creates thorough validation logic
- **Dataclass Usage**: Copilot suggests dataclasses for structured data
- **Custom Exceptions**: Copilot creates meaningful exception classes
- **Test Generation**: Copilot generates pytest test cases

**Example Prompts:**
```
"Create a Python validation function that checks: task has all required fields, 
boardId exists in boards.json, status matches a valid column, timestamps are 
in chronological order, activity IDs are unique. Return a tuple of (is_valid, 
error_messages)."

"Generate a Python dataclass for Task with validation methods and type hints 
for all fields including Optional types where appropriate."

"Write a function that validates timestamp ordering with clear error messages 
explaining what's wrong and suggesting how to fix it."
```

**📌 Key Copilot Learning Points:**
- **Copilot suggests dataclasses**: Better than plain dicts for validation
- **Comprehensive checks**: Copilot thinks of edge cases you might miss
- **Pythonic error handling**: Uses custom exceptions with clear messages
- **Test-driven**: Ask "Create pytest tests for this validation function"

**Example: Add New Task via Python CLI**

**Prompt Copilot to generate this workflow:**

**Using Copilot Chat:**
```
"Create a Python function add_task() that:
1. Loads boards.json to find the tasks file path for a given board
2. Loads existing tasks from the JSON file
3. Creates a new task dictionary with all required fields
4. Generates proper ID using generate_task_id()
5. Adds an initial activity entry with timestamp
6. Appends to tasks list
7. Writes back to file with json.dump() using indent=2
8. Includes type hints and error handling"
```

**Or write comments to guide inline Copilot:**
```python
# Load boards.json to find task file path for specified board

# Load existing tasks from JSON file using context manager

# Create new task dictionary with required fields: id, title, description, status='backlog', etc.

# Add initial activity entry: task created via CLI with timestamp

# Append new task to list

# Write back to file with proper JSON formatting
```

Copilot will generate complete working Python code for each step.

**Example: Move Task Between Columns**

**Prompt Copilot:**

**Using Copilot Chat:**
```
"Create a Python function move_task(task_id: str, new_status: str) that:
1. Loads the appropriate tasks file
2. Finds task by ID in the list
3. Updates status field to new column
4. Sets startedAt timestamp if moving to 'in_progress'
5. Sets completedAt timestamp if moving to 'done'
6. Adds activity entry documenting the status change
7. Saves updated tasks back to file
8. Returns success boolean or raises exception with clear message"
```

**Or use inline comments:**
```python
# Load tasks from JSON file

# Find task in list by ID (use list comprehension or next())

# Save old status for activity log

# Update task status to new column

# Update timestamps: startedAt for in_progress, completedAt for done

# Add activity entry dict with status change details (from/to)

# Save updated tasks list back to JSON file

# Return True or raise ValueError if task not found
```

Copilot generates complete logic including all timestamp handling and activity logging.

**🤖 Copilot Workflow - Complex Multi-File Operations:**

**Copilot Chat Prompt:**
```
"Create a Python function move_task_between_boards(task_id: str, source_board: str, 
target_board: str) that:
1. Loads both source and target task JSON files
2. Finds task by ID in source list, removes it
3. Updates task's boardId and resets status to 'backlog'
4. Adds activity entry logging the board transfer with timestamp
5. Appends task to target list
6. Writes both files atomically (save to temp, then rename)
7. Validates both task lists before writing
8. Includes error handling for: task not found, file errors, validation failures
9. Uses type hints and comprehensive docstring"
```

**Inline Comment Approach:**
```python
# Move task between boards with complete data integrity:
# - Load source_tasks.json and target_tasks.json using Path
# - Find task by ID in source list, remove with list.remove()
# - Update task['boardId'], task['status'], task['updatedAt']
# - Add activity dict with transfer details and ISO timestamp
# - Append to target list
# - Write both files with json.dump(data, f, indent=2)
# - Handle errors: task not found (ValueError), invalid board (FileNotFoundError)
```

Copilot generates complete implementation including all timestamp handling, activity logging, and atomic file operations.

**Validation Checklist to Prompt Copilot:**

**Using Copilot Chat:**
```
"Create a comprehensive Python validation function validate_task(task: dict, 
board_data: dict) that returns a tuple (is_valid: bool, errors: list[str]) 
and checks:
1. Required fields exist (id, title, status, boardId)
2. boardId matches the board being validated against
3. status is a valid column ID from the board's columns
4. Timestamps are in chronological order (createdAt <= startedAt <= completedAt)
5. All activity IDs are unique within the task
6. All timestamp strings are valid ISO 8601 format
Include type hints and detailed docstring."
```

**Or use inline comments:**
```python
# Validate task dictionary has all required fields

# Validate references: boardId matches, status is valid column ID

# Validate timestamp chronological order using datetime.fromisoformat()

# Validate activity IDs are unique (use set to check)

# Return tuple: (bool, list of error message strings)
```

Copilot will generate complete validation logic with detailed, actionable error messages.

**Critical Rules:**
- `createdAt` ≤ `startedAt` ≤ `completedAt`
- `boardId` must exist in boards.json
- `status` must match a column ID in the board
- All timestamps must be valid ISO 8601 format
- Activity IDs must be unique within task
- Task IDs must be unique within file

**Python-Specific Best Practices:**
- Use `pathlib.Path` for cross-platform file paths
- Use context managers (`with open()`) for file operations
- Add type hints to all function parameters and returns
- Write docstrings for all public functions
- Use dataclasses or Pydantic for structured data
- Include logging for debugging CLI operations
- Create a `requirements.txt` if using external packages

**Sample board_manager.py Structure:**
```python
"""Backend data management for ProjectBoard."""

import json
from pathlib import Path
from datetime import datetime, timezone
from typing import Optional

# Constants
DATA_DIR = Path(__file__).parent / "data"
BOARDS_FILE = DATA_DIR / "boards.json"

# Core functions
def load_json_file(file_path: Path) -> dict:
    """Load and parse JSON file safely."""
    pass

def save_json_file(file_path: Path, data: dict) -> None:
    """Save data to JSON file with formatting."""
    pass

def generate_task_id(existing_tasks: list[dict]) -> str:
    """Generate next sequential task ID."""
    pass

def add_task(board_name: str, title: str, description: str = "") -> dict:
    """Add new task to specified board."""
    pass

def move_task(task_id: str, new_status: str) -> bool:
    """Move task to different column."""
    pass

def validate_task(task: dict, board_data: dict) -> tuple[bool, list[str]]:
    """Validate task data integrity."""
    pass
```

---

[← Previous: Phase 7](./phase-07-enterprise-features.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 9 →](./phase-09-testing-refinement.md)
