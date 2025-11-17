# Phase 2: Data Layer Design with Copilot

[← Previous: Phase 1](./phase-01-project-setup.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 3 →](./phase-03-core-logic.md)

---

**Goal:** Use Copilot to design TypeScript interfaces and generate sample data  
**Duration:** ~45 minutes

**Incremental Approach: Build Understanding Layer by Layer**

We'll build the data layer incrementally, starting with simple interfaces and progressively adding complexity. This helps you understand data relationships and lets Copilot's suggestions build on previous context.

### 2.1 Design TypeScript Interfaces with Copilot
- Start with core Task interface
- Add supporting interfaces incrementally
- Refine with Copilot's suggestions
- Build type relationships step-by-step

**🤖 Copilot Techniques:**
- **Description-Driven Generation**: Describe data structure in comments, get interface
- **Inline Completions**: Type `interface Task {` and let Copilot suggest fields
- **Chat for Design**: "What fields should an enterprise task object have?"
- **Iterative Refinement**: Generate basic version, then enhance with Copilot

**Example Prompts:**
```
"Create a TypeScript interface for an enterprise Kanban task with: ID, title, 
description, status, assignee, priority, tags, timestamps (created, updated, 
started, completed), duration estimates, and an activity log array"

"What TypeScript type should I use for ISO 8601 timestamps in JSON?"

"Generate a TaskActivity interface for tracking status changes, comments, 
and system updates with author and timestamp"
```

**📌 Key Learning Points:**
- **Start simple, add complexity**: Basic interface → enterprise fields → relationships
- **Comment-first development**: Write comment describing interface, Copilot generates it
- **Copilot understands enterprise patterns**: Knows common fields for tracking systems
- **Type safety from start**: Copilot suggests appropriate types (string | null vs optional)
- **Incremental refinement**: Accept basic version, enhance with "add priority field", "add tags array"
- **Learning opportunity**: Review each suggestion to understand TypeScript patterns

**Incremental Interface Building:**

**Step 1: Start with minimal Task interface**
- Create new file: `src/types/Task.ts`
- Write a comment: `// Basic task representation`
- Start typing: `interface Task {`
- Press Enter, type `id` and wait for Copilot to suggest the type
- Continue adding fields one by one, letting Copilot help

**Step 2: Ask Copilot to enhance**
- Add comment above interface: `// Add status, assignee, and timestamps`
- Let Copilot suggest the new fields
- Review and accept suggestions that make sense

**Step 3: Add enterprise features incrementally**
- Add comment: `// Add priority (low|medium|high|critical)`
- Add comment: `// Add tags array for categorization`  
- Add comment: `// Add activity log array`
- Let Copilot generate each addition as you type

**Step 4: Refine with Copilot Chat**
- Ask Copilot: "Should completedAt be optional or nullable? What's the difference?"
- Ask Copilot: "Add JSDoc comments explaining each field"
- Review suggestions and apply improvements

**Why This Incremental Approach:**
- ✅ Understand each field's purpose before moving on
- ✅ See how Copilot builds on previous context
- ✅ Learn TypeScript patterns progressively
- ✅ Catch design issues early (easier to fix simple interface)
- ✅ Build confidence with smaller steps

**🎓 Beginner Concept Explanations:**

**What is TypeScript?**
- TypeScript = JavaScript + Types
- Types tell you what kind of data each variable holds
- Example: `title: string` means "title must be text"
- Catches errors before you run the code
- Copilot knows TypeScript and helps you write it correctly

**What is an Interface?**
- A "blueprint" describing what an object should look like
- Lists all properties and their types
- Example: Task interface says every task must have id, title, status, etc.
- TypeScript checks your code matches the interface

**What does `string | null` mean?**
- `|` means "or" in TypeScript
- `string | null` = "either text OR null (nothing)"
- `completedAt: string | null` = "can be a date text or empty"
- Use `null` for optional timestamps that might not exist yet

**What's the difference: `?` vs `| null`?**

**Ask Copilot to show you examples:**
- Prompt: "Show me the difference between optional (?) and nullable (| null) in TypeScript"
- Copilot will generate examples like:
  - `optionalField?: string` = Property might not exist at all
  - `nullableField: string | null` = Property exists, value might be null

**General Rule:**
- Use `?` when the property itself might not be there
- Use `| null` when the property exists but value might be empty  
- For timestamps: use `| null` (property always there, but value might be empty)

**Let Copilot guide you:** As you type field names, Copilot will suggest the appropriate type based on the field name and your comments

✅ **Validation Checkpoint:**
Before moving to Phase 3, verify:
- [ ] Task.ts interface file exists with all required fields
- [ ] No TypeScript errors (check Problems panel in VS Code)
- [ ] You understand what each field represents
- [ ] tasks_main.json has at least 3 sample tasks
- [ ] boards.json file exists and references tasks_main.json
- [ ] All JSON files are valid (no syntax errors - VS Code shows errors in red)

**Copilot Workflow for Interface Design:**

1. **Write descriptive comment first**
   - Type: `/**` then press Enter
   - Copilot generates JSDoc template
   - Fill in: "Represents a task in the Kanban board system"
   - Add details: "Includes enterprise features like time tracking and activity logs"

2. **Start typing interface name**
   - Type: `interface Task {`
   - Press Enter

3. **Let Copilot suggest fields**
   - Copilot will start suggesting common fields
   - Press Tab to accept, or keep typing to modify

4. **Add JSDoc for each field as you go**
   - Type `/**` above a field, Copilot generates documentation
   - This helps Copilot understand your intent for better suggestions

**Copilot Pro Tip: Context is Everything**

**✅ GOOD: Give Copilot detailed context**
- Write a detailed JSDoc comment before your interface
- Include: what it represents, what properties it should have, any constraints
- Example prompt for Copilot Chat: "Create a TaskActivity interface for tracking status changes, comments, and system updates with author and timestamp in ISO 8601 format"
- Result: Copilot suggests rich, appropriate fields

**❌ BAD: No context**
- Just typing `interface TaskActivity {` without comments
- Result: Copilot suggests generic fields that might not fit your needs

**Workflow:**
1. Describe what you need in a comment or Copilot Chat
2. Let Copilot generate the structure
3. Review and refine
4. Ask Copilot to explain if you don't understand a suggestion

### 2.2 Generate JSON Data with Copilot
- Create first task manually with Copilot's help
- Generate variations incrementally
- Build realistic activity logs step-by-step
- Ensure consistency through iteration

**🤖 Copilot Techniques:**
- **Schema-Aware Generation**: With interfaces open, Copilot generates matching JSON
- **Realistic Data**: Copilot creates believable titles, descriptions, usernames
- **Incremental Variety**: Generate one task, then variations
- **Consistency Checking**: Copilot helps maintain valid references

**Example Prompts:**
```
"Create a sample task object matching the Task interface with status 'backlog' 
and high priority"

"Generate a second task for the same board but with status 'in_progress', 
started 2 hours ago, with 2 activity entries"

"Add a third task that's completed, showing the full lifecycle in activity log"

"Create boards.json with main-board configuration referencing tasks_main.json"
```

**Incremental JSON Generation Workflow:**
```
1. Create first task:
   - Open Task interface file for context
   - Create tasks_main.json, type [
   - Comment: "Task in backlog, high priority, auth feature"
   - Let Copilot generate complete object
   - Review: all required fields present? Valid types?

2. Add second task:
   - Type comma after first task
   - Comment: "Task in progress, medium priority, started 2h ago"
   - Copilot generates similar structure with variations
   - Add activity entries incrementally

3. Build activity logs:
   - Start with 1 entry per task
   - Add more: "Add activity entry showing status change"
   - Copilot maintains timestamp chronology

4. Validate incrementally:
   - Check boardId matches
   - Verify status values exist in board columns
   - Ensure timestamps are chronological
   - Ask Copilot: "Does this JSON match the interface?"
```

**📌 Key Learning Points:**
- **One task at a time**: Master structure before adding variety
- **Copilot maintains consistency**: Learns ID patterns, timestamp formats
- **Realistic progression**: Activity logs show natural task evolution
- **Validation while building**: Catch errors early, not after 10 tasks
- **Learn JSON patterns**: Study Copilot's data generation for best practices

**Example Prompts:**
```
"Create a boards.json file with 2 boards: 'main-board' and 'secondary-board', 
each with columns: backlog, in_progress, blocked, review, done. Include WIP 
limits of 3 for in_progress and review"

"Generate 3 realistic tasks for a Kanban board: one in backlog (high priority), 
one in progress (medium priority, started 2 hours ago), one completed (low 
priority, finished yesterday). Include 2-3 activity entries per task"

"Create sample activity entries showing a task moving from backlog → in_progress 
→ review → done with comments from different agents"
```

**📌 Key Learning Points:**
- **Copilot generates realistic content**: Task titles, descriptions are contextual
- **Referential integrity**: Copilot maintains consistent IDs and references
- **Variety in data**: Request different statuses, priorities for comprehensive examples
- **Use interfaces as guide**: Keep TypeScript files open while generating JSON

**Copilot-Assisted Data Generation Workflow:**

1. Open your Task interface file (`Task.ts`) in VS Code
2. Create new file: `data/tasks_main.json`
3. Type opening bracket: `[`
4. Write a comment describing what you need: `// Task in backlog, high priority, auth work`
5. Type `{` and press Enter
6. **Copilot will generate a complete task object** matching your interface
7. Review the generated task, accept if it looks good
8. Repeat: Add another comment for next task, type `{`, Copilot generates
9. Copilot maintains consistency: same field names, proper ID format, valid references

**Pro Tip:** Keep your TypeScript interface file open in a split view while editing JSON - Copilot uses it as context!

**Validating with Copilot:**
```
"Check if all tasks in this file have valid boardId and status references"

"Does this JSON match the Task interface? What's missing?"

"Generate a function to validate that task.boardId exists in boards.json"
```

### 2.3 Data Validation with Copilot
- Generate validation functions with Copilot
- Create type guards with inline suggestions
- Build error messages with Copilot's help
- Test validation with Copilot-generated test cases

**🤖 Copilot Techniques:**
- **Function Generation**: Describe validation logic, get implementation
- **Type Guard Patterns**: Copilot knows TypeScript type guard syntax
- **Error Handling**: Copilot suggests comprehensive error messages
- **Test Generation**: Ask Copilot for validation test scenarios

**Example Prompts:**
```
"Create a type guard function that validates an unknown object matches the 
Task interface with all required fields"

"Generate a validation function that checks if task.boardId exists in the 
boards configuration and task.status matches a valid column ID"

"Write a function that validates timestamp ordering: createdAt must be before 
startedAt which must be before completedAt"
```

**📌 Key Learning Points:**
- **Copilot knows validation patterns**: Generates thorough checks
- **Ask for edge cases**: "What validation errors should I check for?"
- **Incremental validation**: Build validators one concern at a time
- **Learn from Copilot**: Study generated validation logic to improve skills

**🤖 How Copilot Generates Validation Patterns:**

When you write a type comment like:
```javascript
// Create type guard function isValidTask that checks if unknown data is a Task
```

Copilot generates:
- Complete type guard with proper TypeScript syntax
- Type checks for all fields (typeof, Array.isArray)
- Null handling for optional timestamps
- Array validation for activity entries
- String format checks for IDs and statuses

**Ask Copilot in Chat:**
```
"Generate a type guard function that validates if unknown JSON data 
matches the Task interface. Include checks for required fields, 
optional timestamps, and activity array."
```

---

[← Previous: Phase 1](./phase-01-project-setup.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 3 →](./phase-03-core-logic.md)
