# Phase 5: Rendering Engine with Copilot

[← Previous: Phase 4](./phase-04-ui-foundation.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 6 →](./phase-06-interactive-features.md)

---

**Goal:** Use Copilot to generate efficient DOM manipulation code  
**Duration:** ~60 minutes

### 5.1 Board Rendering with Copilot
- Generate rendering functions with Copilot
- Use Copilot for DocumentFragment patterns
- Get DOM manipulation best practices
- Copilot-assisted template literals

**🤖 Copilot Techniques:**
- **Template Literals**: Copilot generates clean HTML template strings
- **DOM Patterns**: Copilot knows DocumentFragment for performance
- **Loop-based Rendering**: Copilot converts data arrays to DOM elements
- **Event Delegation**: Copilot suggests efficient event handling patterns

**Example Prompts:**
```
"Create a function that renders board columns from a Board object using 
DocumentFragment for performance, adding proper ARIA labels and data attributes"

"Generate a renderBoardSelector function that populates a dropdown with 
boards from BoardsConfig and handles selection events"

"Write code that clears the board container and renders new columns without 
causing layout thrashing"
```

**📌 Key Copilot Learning Points:**
- **Copilot knows performance patterns**: Suggests batching, fragments, avoiding reflows
- **Template string expertise**: Copilot generates readable multi-line HTML
- **Event handling**: Copilot adds event listeners with proper cleanup
- **Incremental learning**: Accept Copilot suggestion, then ask "Why use DocumentFragment?"

**🎓 Beginner Concept Explanations:**

**What is the DOM?**
- DOM = Document Object Model
- Your HTML turned into JavaScript objects
- JavaScript can read and modify the DOM to change the page
- Example: `document.querySelector('.board')` finds the board element
- Example: `element.innerHTML = 'new text'` changes what's inside

**What is DocumentFragment?**
- Temporary container for building HTML in memory
- Faster than adding elements one-by-one to the page
- Think of it like: assemble LEGO set in box, then put finished set on shelf
- vs: adding each LEGO piece to shelf one at a time (slow!)

**What is innerHTML vs createElement?**

**Ask Copilot to show you examples:**
- Prompt: "Show me the difference between innerHTML and createElement in JavaScript with examples"
- Copilot will generate examples of both approaches

**General Guidelines:**
- Use innerHTML for complete replacement of content
- Use createElement for adding specific elements
- **Never** use innerHTML with user input (XSS security risk!)

**Let Copilot guide your choice:**
- Comment: `// Replace content safely without XSS risk`
- Copilot will suggest createElement or escapeHtml approaches

**What is XSS?**
- XSS = Cross-Site Scripting (security attack)
- Attacker puts `<script>` tags in task description
- If you use innerHTML, the script runs (bad!)
- **Always** escape user content or use textContent instead
- Example: `escapeHtml(task.description)` removes dangerous characters

**Rendering Pattern to Prompt Copilot:**

**Write these comments in your render function, let Copilot generate the code:**

```
// 1. Clear existing content from board container

// 2. Create document fragment for efficient rendering

// 3. Loop through board columns and create elements

// 4. Add all elements to fragment

// 5. Add fragment to DOM in single operation
```

**Copilot will generate:**
- `boardContainer.innerHTML = ''` to clear
- `document.createDocumentFragment()` for efficiency
- `.forEach()` loop for columns
- `.appendChild()` calls
- Final single DOM insertion

**Or ask Copilot Chat:**
"Create a function that efficiently renders board columns using DocumentFragment to minimize DOM reflows"

**Why This Pattern?**
- ❌ BAD: Adding elements one-by-one triggers page redraw each time (slow)
- ✅ GOOD: Build in fragment, add once = single redraw (fast)
- Matters when rendering 50+ tasks

✅ **Validation Checkpoint:**
Before moving to Phase 6, verify:
- [ ] Board renders correctly with all columns visible
- [ ] Tasks appear in correct columns
- [ ] Task cards show all information (title, assignee, times, etc.)
- [ ] No XSS vulnerabilities (test with task description: `<script>alert('test')</script>` - should display as text, not run)
- [ ] Page renders smoothly even with 20+ tasks
- [ ] Console shows no errors during render
- [ ] Activity logs display correctly formatted

**WIP Limit Display Logic:**
- Show count if `wipLimit` is not null
- Highlight red when at/over limit
- Show as "3/3" (current/limit) format
- Update dynamically as tasks move

### 5.2 Task Rendering with Copilot
- Generate task card HTML with Copilot
- Use Copilot for conditional rendering logic
- Get time formatting helpers from Copilot
- Copilot-assisted XSS prevention

**🤖 Copilot Techniques:**
- **Complex Templates**: Copilot handles multi-part card structures
- **Conditional Rendering**: Copilot adds if/else for optional fields
- **String Formatting**: Copilot creates human-readable time displays
- **Security Awareness**: Copilot suggests escaping user content

**Example Prompts:**
```
"Create a renderTaskCard function that generates a Bootstrap card with task 
title, description, priority badge, assignee, elapsed time, and shows 
completedAt only if task is done"

"Write a function that formats ISO 8601 timestamps as relative time 
(e.g., '2 hours ago') using Intl.RelativeTimeFormat"

"Generate an escapeHtml utility function to prevent XSS when displaying 
user-generated task descriptions"
```

**📌 Key Copilot Learning Points:**
- **Copilot handles complexity**: Builds multi-section components systematically
- **Security conscious**: Often includes HTML escaping in generated code
- **API knowledge**: Copilot uses modern browser APIs like Intl formatters
- **Ask for improvements**: "Make this more accessible" or "Add loading states"

**Copilot Workflow Example:**

1. **Write function signature with JSDoc**
   - Type: `/** Renders a task card DOM element with priority indicator and time tracking */`
   - Press Enter, start typing: `function renderTaskCard(task: Task): HTMLElement {`

2. **Let Copilot suggest implementation**
   - Copilot will suggest creating element, building template, returning
   - Accept the overall structure

3. **Refine specific parts with comments**
   - Add comment: `// Add XSS protection for description`
   - Copilot suggests using `escapeHtml()` or `textContent`

4. **Build incrementally**
   - Comment: `// Add priority badge in header`
   - Comment: `// Add time tracking display`
   - Comment: `// Add activity preview`
   - Copilot generates each section

**Task Card Structure Decision:**
```
┌─────────────────────────────────────┐
│ [PRIORITY BADGE] Title              │ ← Header
├─────────────────────────────────────┤
│ Description text...                 │ ← Body
│                                     │
│ 👤 Assignee  ⏱️ 2h 30m elapsed     │ ← Metadata
│ 🏷️ tag1, tag2                      │
├─────────────────────────────────────┤
│ 📝 Activity (2 entries)            │ ← Footer
└─────────────────────────────────────┘
```

**Time Display Formatting:**
- Use `Intl.RelativeTimeFormat` for relative times
- Show absolute dates on hover (tooltip)
- Format durations as "2h 30m" not "150 minutes"
- Update elapsed times periodically (every minute)

**Critical Rendering Functions to Prompt Copilot:**

**Ask Copilot to generate these functions:**

1. **createTaskCard** - Comment: `// Create task card HTML element with all task details`
2. **formatDuration** - Comment: `// Format minutes as '2h 30m' human-readable string`
3. **formatRelativeTime** - Comment: `// Format ISO timestamp as relative time using Intl.RelativeTimeFormat`
4. **escapeHtml** - Comment: `// Escape HTML special characters to prevent XSS attacks`

**Or use Copilot Chat:**
"Create four utility functions for rendering tasks: createTaskCard, formatDuration, formatRelativeTime, and escapeHtml for XSS protection"

### 5.3 Activity Log Rendering
- `renderTaskActivity()` - Display activity entries
- Format timestamps for readability
- Differentiate activity types (status_update, comment, system)
- Show author information

**📌 Key Points:**
- **Chronological order**: Most recent first or last? → Last (natural reading)
- **Activity icons**: Different icon per type (🔄 status, 💬 comment, ⚙️ system)
- **Compact display**: Show only last N entries by default
- **Expandable**: "Show all activity" option for full history
- **Color coding**: Subtle background colors per activity type

**Activity Entry Rendering:**
```html
<!-- Status Update -->
<div class="activity-entry status-update">
  <span class="activity-icon">🔄</span>
  <span class="activity-author">agent-alpha</span>
  <span class="activity-message">
    moved from <strong>Backlog</strong> to <strong>In Progress</strong>
  </span>
  <time class="activity-time">2 hours ago</time>
</div>

<!-- Comment -->
<div class="activity-entry comment">
  <span class="activity-icon">💬</span>
  <span class="activity-author">agent-beta</span>
  <span class="activity-message">API endpoint is ready</span>
  <time class="activity-time">1 hour ago</time>
</div>
```

**Activity Type Formatting:**
- `status_update`: Show from → to transition
- `comment`: Display message as-is
- `system`: Italic text, muted color
- Include timestamp in all entries

---

[← Previous: Phase 4](./phase-04-ui-foundation.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 6 →](./phase-06-interactive-features.md)
