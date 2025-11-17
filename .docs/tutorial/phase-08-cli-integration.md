# Phase 8: CLI Integration Design with Copilot

[← Previous: Phase 7](./phase-07-enterprise-features.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 9 →](./phase-09-testing-refinement.md)

---

**Goal:** Use Copilot to design and document CLI interaction patterns  
**Duration:** ~30 minutes

### 8.1 CLI Documentation with Copilot
- Generate integration documentation with Copilot Chat
- Use Copilot for code example generation
- Get best practices from Copilot
- Copilot-assisted specification writing

**🤖 Copilot Techniques:**
- **Documentation Generation**: Copilot writes technical docs from code
- **Example Code**: Copilot creates complete, runnable examples
- **Pattern Library**: Copilot knows common CLI interaction patterns
- **Multi-language**: Copilot can show examples in Node.js, Python, etc.

**Example Prompts:**
```
"Write documentation explaining how a CLI tool should interact with the 
boards.json and task files, including ID generation conventions and 
timestamp format requirements"

"Generate a Node.js example showing how to add a new task to tasks_main.json 
with proper validation and activity entry creation"

"Create documentation for CLI best practices when modifying JSON files: 
read, validate, modify, write pattern"
```

**📌 Key Copilot Learning Points:**
- **From code to docs**: Copilot reads your interfaces and generates documentation
- **Complete examples**: Copilot creates working code, not just snippets
- **Best practices included**: Copilot adds error handling, validation in examples
- **Ask for clarity**: "Explain this in simpler terms for beginners"

**ID Generation Convention:**

**ID Formats:**
- Task IDs: `task-001`, `task-002`, `task-003`, etc.
- Activity IDs: `act-001`, `act-002`, etc.
- Epic IDs: `epic-001`, `epic-002`, etc.

**Prompt Copilot to generate ID function:**
- Comment: `// Generate next task ID in format task-XXX by finding max ID and incrementing`
- Start typing: `function generateTaskId(existingTasks: Task[]): string {`
- Copilot will suggest logic to:
  - Extract numbers from existing IDs
  - Find maximum ID
  - Add 1
  - Format with zero-padding (3 digits)

**Or ask Copilot Chat:**
"Create a function that generates sequential task IDs in format task-001 by finding the highest existing ID number and adding 1"

**Timestamp Conventions:**

**Format: ISO 8601 (UTC timezone)**
- Example: `"2025-11-17T10:30:00.000Z"`

**Prompt Copilot for timestamps:**
- Comment: `// Generate current timestamp in ISO 8601 format`
- Copilot suggests: `new Date().toISOString()`

**For activity entries:**
- Comment: `// Create activity object with current ISO timestamp`
- Copilot generates complete object with proper timestamp field

**Ask Copilot Chat:**
"How do I generate ISO 8601 formatted timestamps in JavaScript for activity log entries?"

### 8.2 CLI Code Examples with Copilot
- Generate CLI scripts with Copilot
- Use Copilot for file I/O operations
- Get validation logic from Copilot
- Copilot-assisted error handling

**🤖 Copilot Techniques:**
- **Complete Script Generation**: Copilot writes full Node.js scripts
- **File Operations**: Copilot handles fs module operations correctly
- **JSON Safety**: Copilot adds try/catch for JSON.parse
- **Cross-platform**: Copilot uses path.join for file paths

**Example Prompts:**
```
"Create a Node.js script that adds a new task to a board: reads boards.json 
to find task file, loads tasks, generates new task with all required fields, 
appends it, and writes back with formatting"

"Generate a CLI tool function that moves a task between columns by updating 
its status field, adding activity entry, and handling startedAt/completedAt 
timestamps appropriately"

"Write a script that moves a task from one board's task file to another, 
updating boardId and maintaining referential integrity"
```

**📌 Key Copilot Learning Points:**
- **Copilot writes working code**: Generated scripts actually run
- **Imports included**: Copilot adds necessary require/import statements
- **Error handling built-in**: Copilot includes file existence checks, JSON validation
- **Learn Node.js**: Study Copilot's fs and path module usage

**🤖 Copilot Workflow for CLI Scripts:**

**Step 1: Write complete workflow comment**
```javascript
/**
 * CLI script to add new task to specified board
 * Usage: node add-task.js --board main-board --title "Task title"
 * Steps:
 * 1. Parse command line arguments
 * 2. Load tasks JSON file for specified board
 * 3. Create new task with generated ID
 * 4. Add to tasks array
 * 5. Write back to file with proper formatting
 */
```

**Step 2: Copilot suggests imports**
```javascript
// Import Node.js modules needed for file operations and argument parsing
```
Copilot adds: `const fs = require('fs'); const path = require('path');`

**Step 3: Write function signature**
```javascript
// Function to add task to board: loads file, validates, adds task, saves
```

**Step 4: Copilot implements complete logic** including error handling, validation, and file I/O

### 8.3 Data Integrity Validation with Copilot
- Generate validation functions with Copilot
- Use Copilot for comprehensive checks
- Get test cases from Copilot
- Copilot-assisted error messaging

**🤖 Copilot Techniques:**
- **Validation Generators**: Copilot creates thorough validation logic
- **Edge Case Coverage**: Copilot suggests validations you might miss
- **Error Messages**: Copilot writes clear, actionable error text
- **Test Cases**: Copilot generates test data for validation

**Example Prompts:**
```
"Create a comprehensive validation function that checks: task has all 
required fields, boardId exists in boards.json, status matches a valid 
column, timestamps are in correct order, activity IDs are unique"

"Generate validation rules for CLI scripts: what checks should run before 
writing modified JSON back to file?"

"Write a function that validates timestamp ordering with clear error 
messages explaining what's wrong and how to fix it"
```

**📌 Key Copilot Learning Points:**
- **Copilot thinks comprehensively**: Suggests validations you might forget
- **User-friendly errors**: Copilot writes helpful error messages, not just "invalid"
- **Test generation**: Ask "Create test cases for this validation function"
- **Learn validation patterns**: Study Copilot's approach to data integrity

**Example: Add New Task via CLI**

**Prompt Copilot to generate this workflow:**

**Using Copilot Chat:**
"Create a Node.js script that:
1. Loads boards.json to find the tasks file path
2. Loads existing tasks from the file
3. Creates a new task object with all required fields
4. Generates proper IDs (use generateTaskId function)
5. Adds an initial activity entry
6. Appends to tasks array
7. Writes back to file with pretty formatting (2-space indent)"

**Or write comments to guide inline Copilot:**
```
// Load boards.json to find task file path for main-board

// Load existing tasks from file

// Create new task object with required fields: id, title, description, status=backlog, etc.

// Add initial activity entry: task created via CLI

// Append new task to array

// Write back to file with JSON.stringify formatting
```

Copilot will generate complete working code for each step.

**Example: Move Task Between Columns**

**Prompt Copilot:**

**Using Copilot Chat:**
"Create a function that moves a task between Kanban columns by:
1. Finding task by ID
2. Updating status field to new column
3. Setting startedAt timestamp if moving to in_progress
4. Setting completedAt timestamp if moving to done  
5. Adding activity entry documenting the status change
6. Writing updated tasks back to file"

**Or use inline comments:**
```
// Find task in array by ID

// Save old status for activity log

// Update task status to new column

// Update timestamp: startedAt if moving to in_progress, completedAt if moving to done

// Add activity entry with status change details (from/to)

// Write updated tasks array back to file
```

Copilot generates complete logic including all timestamp handling and activity logging.

**🤖 Copilot Workflow - Complex Multi-File Operations:**

**Copilot Chat Prompt:**
```
"Create a function to move a task between boards:
1. Load both source and target task JSON files
2. Find task by ID in source, remove it
3. Update task's boardId and reset status to 'backlog'
4. Add activity entry logging the board transfer
5. Add task to target file
6. Write both files atomically
7. Validate both before writing

Include error handling for: task not found, file read/write errors, validation failures."
```

**Inline Comment Approach:**
```javascript
// Move task between boards with complete data integrity:
// - Load tasks_main.json and tasks_secondary.json
// - Find task by ID, remove from source array
// - Update task.boardId, task.status, task.updatedAt
// - Add activity entry with transfer details
// - Push to target array
// - Write both files with JSON.stringify(data, null, 2)
// - Handle errors: task not found, invalid board ID
```

Copilot generates complete implementation including all timestamp handling and activity logging.

**Validation Checklist to Prompt Copilot:**

**Using Copilot Chat:**
"Create a comprehensive task validation function that returns an object with {valid: boolean, errors: string[]} and checks:
1. Required fields exist (id, title, status, boardId)
2. boardId matches the current board
3. status is a valid column ID from the board
4. Timestamps are in chronological order (createdAt ≤ startedAt ≤ completedAt)
5. All activity IDs are unique within the task"

**Or use inline comments:**
```
// Validate task has all required fields

// Validate references: boardId exists, status is valid column

// Validate timestamp chronological order

// Validate activity IDs are unique

// Return validation result object with errors array
```

Copilot will generate complete validation logic with detailed error messages.

**Critical Rules:**
- `createdAt` ≤ `startedAt` ≤ `completedAt`
- `boardId` must exist in boards.json
- `status` must match a column ID in the board
- All timestamps must be valid ISO 8601
- Activity IDs must be unique within task
- Task IDs must be unique within file

---

[← Previous: Phase 7](./phase-07-enterprise-features.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 9 →](./phase-09-testing-refinement.md)
