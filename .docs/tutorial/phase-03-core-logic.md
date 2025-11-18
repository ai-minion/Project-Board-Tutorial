# Phase 3: Core Application Logic with Copilot

[← Previous: Phase 2](./phase-02-data-layer.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 4 →](./phase-04-ui-foundation.md)

---

**Goal:** Build logic for frontend (TypeScript) and understand backend separation  
**Duration:** ~60 minutes  
**Focus:** TypeScript functions for browser-side data operations

**Architecture Reminder:**
- **This Phase (Frontend)**: TypeScript functions that run in the browser
- **Data Loading**: Fetch and parse JSON files for display
- **Data Transformation**: Filter, sort, calculate for UI purposes
- **Backend (Python)**: Handles actual file writes (covered in Phase 8)

### 3.1 Data Loading Module with Copilot (TypeScript - Frontend)
- Use Copilot to generate async fetch functions
- Get error handling suggestions from Copilot
- Generate type guards with Copilot's help
- Refine loading states with Copilot

**🤖 Copilot Techniques:**
- **Function Signatures First**: Write signature with JSDoc, Copilot completes body
- **Error Handling Patterns**: Copilot suggests try/catch and error messages
- **Async/Await Mastery**: Copilot knows modern async patterns
- **Type Guards**: Copilot generates validation logic from interfaces

**Example Prompts:**
```
"Create an async function that fetches boards.json, parses it, validates 
it matches BoardsConfig interface, and returns it with proper error handling"

"Generate a type guard function that checks if parsed JSON is a valid 
BoardsConfig object"

"Write a function that loads tasks from a dynamic file path with retry 
logic on failure"
```

**📌 Key Copilot Learning Points:**
- **Start simple, add complexity**: Basic function → error handling → edge cases
- **Comment-driven development**: Write what function should do, Copilot implements it
- **Copilot suggests error handling**: Often includes edge cases you might miss
- **Pattern recognition**: Copilot applies best practices from similar codebases
- **Iterative improvement**: Generate basic version → test → ask "add error handling" → enhance
- **One function at a time**: Master data loading before transformation

**🎯 Important: Frontend vs Backend Logic**

**Frontend (This Phase - TypeScript):**
- ✅ **Read** JSON files via fetch()
- ✅ **Display** data in the browser
- ✅ **Filter/sort** for viewing
- ✅ **Client-side validation** before sending to backend
- ❌ **No writing** to JSON files (browser can't directly write files)

**Backend (Phase 8 - Python):**
- ✅ **Read** JSON files via pathlib
- ✅ **Write** JSON files safely
- ✅ **Data integrity** validation
- ✅ **CLI tools** for task management

**Why This Split?**
- Browsers cannot write to local files for security reasons
- Python `board_manager.py` handles all file modifications
- TypeScript reads JSON and displays it
- Users interact with UI → data sent to Python → Python updates files → TypeScript re-reads

**Incremental Function Building:**

**Step 1: Basic function signature**
- Write JSDoc comment: `/** Loads board configuration from boards.json */`
- Start typing: `async function loadBoardsConfig()`
- Let Copilot suggest the basic implementation

**Step 2: Add type safety**
- Add comment above function: `// Add return type and validate against BoardsConfig interface`
- Copilot will suggest: `Promise<BoardsConfig>` return type
- Copilot adds validation logic

**Step 3: Add error handling**
- Add comment inside function: `// Add try/catch for network errors and JSON parsing errors`
- Copilot wraps existing code in try/catch block

**Step 4: Add user feedback**
- Add comment: `// Add console logging for debugging`
- Copilot adds appropriate console.log statements

**Step 5: Test and refine**
- Run the function, see what breaks
- Ask Copilot Chat: "How can I improve error messages in this function?"
- Copilot suggests improvements based on your code

**🎓 Beginner Concept Explanations:**

**What is async/await?**
- Used for operations that take time (loading files, network requests)
- `async` = "this function does something that takes time"
- `await` = "wait for this to finish before continuing"
- Like ordering coffee: you `await` your drink before you can drink it
- Copilot automatically adds async/await when needed

**What is fetch()?**
- Built-in browser function to load files
- `fetch('boards.json')` = "go get the boards.json file"
- Returns a Promise ("I promise to get this for you")
- Use with `await` to wait for the file to load

**What is JSON?**
- JSON = JavaScript Object Notation
- Text format for storing data
- Looks like JavaScript objects: `{"name": "value"}`
- `JSON.parse()` converts JSON text to JavaScript object
- `JSON.stringify()` converts JavaScript object to JSON text

**What is a type guard?**
- Function that checks if data matches expected structure
- Returns `true` if valid, `false` if not
- Example: `isValidTask()` checks if object has all Task fields
- Prevents errors from bad data

**Common Pitfalls to Avoid:**

**Ask Copilot to show you the difference:**
- Prompt in Copilot Chat: "Show me the difference between blind type assertion and validated type assertion in TypeScript"
- Copilot will generate examples of both patterns

**❌ BAD: Blind type assertion**
- Trusting data without checking
- Problem: If data is wrong, TypeScript won't catch it!

**✅ GOOD: Validate then assert**  
- Check data first with a validation function
- Then safely assert the type
- Copilot will suggest this pattern when you write validation logic

**How to get Copilot to generate the good pattern:**
- Write comment: `// Validate JSON data before using it`
- Start typing your fetch code
- Copilot will suggest validation checks before type assertions

**Error Handling Strategy:**
- **Network errors** → User-friendly message + retry option
  - Example: "Could not load boards. Check your internet connection."
- **Parse errors** → Log full error, show "invalid data" message
  - Example: "boards.json has invalid syntax. Check for missing commas."
- **Validation errors** → Specific error with location (which board/task)
  - Example: "Task 'task-001' has invalid status 'wrong-status'"

✅ **Validation Checkpoint:**
Before moving to Phase 4, verify:
- [ ] Can successfully load boards.json (no errors in console)
- [ ] Can load tasks from tasks_main.json
- [ ] Console.log() shows loaded data correctly
- [ ] Invalid JSON shows error message (test by breaking JSON temporarily)
- [ ] TypeScript compilation succeeds (`npm run build` works)
- [ ] All async functions have try/catch error handling

### 3.2 Data Transformation with Copilot
- Generate pure functions with Copilot inline suggestions
- Use Copilot Chat for complex algorithms
- Get Copilot's help with array methods and functional patterns
- Optimize performance with Copilot suggestions

**🤖 Copilot Techniques:**
- **Pure Function Generation**: Copilot excels at stateless transformations
- **Array Method Mastery**: Copilot suggests filter, map, reduce patterns
- **Time Calculations**: Copilot handles date math and duration logic
- **Multi-Step Logic**: Break complex functions into steps, Copilot implements each

**Example Prompts:**
```
"Create a pure function that filters tasks by column status and sorts by 
priority (critical > high > medium > low) then by createdAt"

"Write a function that calculates elapsed time in minutes between a task's 
startedAt timestamp and now, returning null if not started"

"Generate a calculateTaskMetrics function that computes actualDuration, 
elapsedTime, and remainingTime based on task timestamps and estimates"
```

**📌 Key Copilot Learning Points:**
- **Copilot knows functional patterns**: Filter, map, reduce, sort combinations
- **Math operations**: Copilot handles date arithmetic and time zone logic
- **Edge cases**: Copilot often suggests null checks and validation
- **Performance awareness**: Request optimizations: "Make this function efficient for 1000+ tasks"

**Key Calculations to Prompt Copilot:**

**1. Actual Duration (completed tasks only)**
- Write comment: `// Calculate actual duration: completedAt - startedAt in minutes, only if both timestamps exist`
- Copilot generates date math and null checks

**2. Elapsed Time (in-progress tasks)**  
- Write comment: `// Calculate elapsed time: current time - startedAt in minutes, update in real-time`
- Copilot generates calculation with `Date.now()`

**3. Time Remaining**
- Write comment: `// Calculate time remaining: estimatedDurationMinutes - elapsedMinutes (can be negative if over estimate)`
- Copilot handles the subtraction and negative cases

**4. Overdue Detection**
- Write comment: `// Check if task is overdue: if dueAt exists and current time > dueAt, handle differently for completed vs in-progress`
- Copilot generates conditional logic

**Or ask Copilot Chat:**
"Create functions to calculate task time metrics: actual duration, elapsed time, time remaining, and overdue status"

**Priority Sorting Logic to Prompt:**

**Ask Copilot to generate sorting:**
- Comment: `// Sort tasks by priority (critical > high > medium > low), then by createdAt oldest first`
- Comment: `// Blocked tasks get visual indicator but stay in priority order`

Copilot will generate:
- Priority order mapping
- Comparison function for sorting
- Chronological sort within same priority

**Or use Copilot Chat:**
"Create a function that sorts tasks by priority level (critical, high, medium, low) and within each priority by creation date oldest first"

### 3.3 Board Management Module
- `getCurrentBoard()` - Get active board state
- `switchBoard()` - Handle board selection changes
- `validateBoardData()` - Ensure data integrity

**📌 Key Points:**
- **State management**: Track current board ID in module-level variable
- **Reload efficiency**: Only reload tasks when board actually changes
- **Persistence**: Save board selection to localStorage
- **Cross-board validation**: Ensure task references are valid when switching

**State Management Pattern:**

**Prompt Copilot to create state management:**

**Write comments to guide Copilot:**
```
// Module-level state variables for current board
// - currentBoardId (string or null)
// - currentBoardData (Board or null)  
// - currentTasks (Task array)
```

Copilot will generate the variable declarations.

**Then prompt for state management functions:**
- Comment: `// Function to clear all state when switching boards`
- Comment: `// Function to reload board data efficiently`
- Comment: `// Function to update UI after state changes`

Copilot generates the implementation for each.

---

[← Previous: Phase 2](./phase-02-data-layer.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 4 →](./phase-04-ui-foundation.md)
