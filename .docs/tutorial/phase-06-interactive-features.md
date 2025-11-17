# Phase 6: Interactive Features with Copilot

[← Previous: Phase 5](./phase-05-rendering-engine.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 7 →](./phase-07-enterprise-features.md)

---

**Goal:** Use Copilot to implement event handling and state management  
**Duration:** ~45 minutes

### 6.1 Board Selection with Copilot
- Generate event handlers with Copilot
- Use Copilot for loading state UI
- Get error recovery patterns from Copilot
- Copilot-assisted state management

**🤖 Copilot Techniques:**
- **Event Handler Generation**: Copilot writes complete event handling logic
- **State Management**: Copilot suggests patterns for tracking app state
- **Loading States**: Copilot adds spinner/disabled UI during async operations
- **Error Boundaries**: Copilot includes try/catch with user-friendly messages

**Example Prompts:**
```
"Create an event handler for board selector change that shows a loading 
spinner, fetches new board tasks, validates data, updates UI, and handles 
errors gracefully"

"Write a switchBoard function that saves selection to localStorage and 
reverts to previous board if loading fails"

"Generate code that disables the board selector during task loading to 
prevent race conditions"
```

**📌 Key Copilot Learning Points:**
- **Complete workflows**: Copilot thinks through entire user interaction flow
- **Edge case handling**: Copilot adds error handling, loading states, race condition prevention
- **localStorage patterns**: Copilot knows browser storage APIs
- **Learn from Copilot**: Study generated async flows to understand best practices

**🤖 Copilot Workflow - Board Switch Implementation:**

Write the flow as comments, Copilot generates the code:
```javascript
// 1. User selects new board from dropdown
// 2. Show loading indicator while fetching
// 3. Fetch tasks for new board from JSON file
// 4. Validate task data against interface
// 5. Update application state with new board data
// 6. Re-render all columns and tasks
// 7. Hide loading indicator
// 8. Save selection to localStorage for persistence
```

Copilot generates the complete async workflow including error handling.

**Error Recovery Pattern (via Copilot):**
```javascript
// Handle board switch errors:
// - Revert dropdown to previous selection
// - Show user-friendly error message
// - Keep current board displayed
// - Log error to console for debugging
```

### 6.2 Live Reload Integration with Copilot
- Use Copilot to configure development tools
- Generate localStorage persistence code
- Get Copilot suggestions for state preservation
- Copilot-assisted configuration files

**🤖 Copilot Techniques:**
- **Tool Configuration**: Copilot knows live-server and similar tool configs
- **State Persistence**: Copilot generates localStorage get/set with JSON parse/stringify
- **Initialization Logic**: Copilot writes app startup code that restores state
- **Development vs Production**: Copilot can suggest environment-specific code

**Example Prompts:**
```
"Create functions to save and restore board selection from localStorage 
with error handling for corrupted data"

"Generate app initialization code that loads saved board from localStorage 
or defaults to first board if no saved state"

"What live-server configuration do I need to watch both JSON files and 
compiled TypeScript output?"
```

### 6.3 Real-time Calculations with Copilot
- Generate interval-based update logic with Copilot
- Use Copilot for efficient DOM updates
- Get performance optimization suggestions
- Copilot-assisted Page Visibility API integration

**🤖 Copilot Techniques:**
- **Interval Management**: Copilot handles setInterval with proper cleanup
- **Selective Updates**: Copilot suggests updating only changed elements
- **Performance APIs**: Copilot knows requestAnimationFrame and Page Visibility
- **Memory Management**: Copilot includes cleanup functions

**Example Prompts:**
```
"Create a real-time update system that refreshes elapsed times every minute 
using setInterval, with cleanup function and pause when tab is hidden"

"Write a function that updates only tasks in 'in_progress' status with new 
elapsed times without re-rendering entire board"

"Generate code using Page Visibility API to pause updates when user switches tabs"
```

**📌 Key Copilot Learning Points:**
- **Cleanup awareness**: Copilot includes clearInterval and event listener removal
- **Performance conscious**: Copilot suggests batching updates, avoiding unnecessary work
- **Browser API knowledge**: Copilot knows modern APIs like Page Visibility
- **Ask for explanations**: "Why pause updates when tab is hidden?" gets educational response

---

[← Previous: Phase 5](./phase-05-rendering-engine.md) | [↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 7 →](./phase-07-enterprise-features.md)
