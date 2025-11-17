# Phase 1: Project Setup & Foundation with Copilot

[↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 2 →](./phase-02-data-layer.md)

---

**Goal:** Learn how to structure projects for optimal Copilot assistance  
**Duration:** ~30 minutes

**Tutorial Approach: Incremental Learning**
This tutorial uses a **step-by-step incremental approach** where you build each piece with Copilot's help, understanding why each part exists and how it works. While Copilot's `/new` command can scaffold entire projects instantly, we'll build incrementally to maximize learning.

### 1.1 Configure GitHub Copilot Custom Instructions

**🎯 Goal:** Create a `.github/copilot-instructions.md` file to provide project-specific context to Copilot

**Why This Matters:**
Custom instructions are **automatically included in the context with every Copilot message**—both inline suggestions and chat interactions. This means Copilot understands your project's architecture, conventions, and preferences in every single interaction, resulting in consistently relevant suggestions throughout development without you having to repeat yourself.

**📖 Reference:** [GitHub Docs: Add repository instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)

**🤖 Copilot Techniques:**
- **Project Context**: Define architecture patterns and tech stack
- **Conventions**: Specify naming, formatting, and coding standards
- **Preferences**: Guide Copilot toward your preferred approaches

**Example Prompts:**
```
"Create a .github/copilot-instructions.md file that explains this is a 
TypeScript Kanban board using Bootstrap 5, JSON data files, and strict 
TypeScript mode with enterprise task tracking features"

"Add coding conventions to copilot-instructions.md: use functional 
programming, avoid 'any' types, prefer const over let, use JSDoc comments"
```

**Custom Instructions Template:**
```markdown
# GitHub Copilot Custom Instructions

## Project Overview
This is an enterprise Kanban board application built with TypeScript, 
Bootstrap 5, and JSON-based data storage. Focus on clean, typed code 
with comprehensive documentation.

## Technology Stack
- TypeScript (strict mode enabled)
- Bootstrap 5.3.8 for UI components
- Vanilla JavaScript DOM manipulation
- JSON files for data persistence
- live-server for development

## Coding Conventions
- Use TypeScript strict mode (no `any` types)
- Prefer functional programming patterns
- Use `const` over `let` where possible
- All functions must have JSDoc comments
- Use semantic HTML5 elements
- Follow Bootstrap utility-first approach

## Architecture Patterns
- Separate concerns: data layer, business logic, UI rendering
- Pure functions for data transformations
- Event delegation for dynamic content
- DocumentFragment for batch DOM operations
- Interfaces for all data structures

## File Naming
- TypeScript: PascalCase for interfaces, camelCase for functions
- JSON: lowercase with hyphens (boards.json, tasks_main.json)
- CSS: kebab-case for class names

## Preferences
- Prioritize code clarity over brevity
- Include error handling in all async operations
- Add accessibility attributes (ARIA) to interactive elements
- Generate comprehensive JSDoc with @param, @returns, @example
```

**📌 Key Learning Points:**
- **Create before coding**: Set up instructions before generating code
- **Update as you build**: Refine instructions when patterns emerge
- **Be specific**: Detailed instructions = better suggestions
- **Include examples**: Show Copilot your preferred code style

### 1.2 Initialize Project Structure with Copilot

**Technology Stack (Latest Versions - November 2025):**
- **TypeScript**: 5.9.3 (latest stable)
- **Bootstrap**: 5.3.8 (latest stable)
- **Node.js**: 20+ LTS (v24.11.1 recommended)
- **Dev Server**: Vite 7.2.2 (recommended) OR live-server 1.2.2 (simpler)

**🤖 Copilot Techniques:**
- **Context Setting**: Open Copilot Chat and describe your project goals
- **Targeted Prompts**: Request one file/config at a time
- **File Generation**: Ask Copilot to create specific configuration files
- **Best Practices**: Request modern TypeScript configurations with explanations
- **Incremental Building**: Add complexity step-by-step, letting Copilot guide you

**Example Prompts:**
```
"What directory structure do you recommend for a TypeScript Kanban board 
with separate documentation?"

"Create a tsconfig.json for a TypeScript 5.9 project that compiles to ES2022 
with strict mode enabled, outputting to a dist folder, using modern module resolution"

"Generate a package.json with TypeScript, live-server, and development 
scripts for watch mode and serving"

"Create a .gitignore file for a TypeScript project with Node.js"
```

**Incremental Workflow:**
```
1. Create .github directory in project root
2. Create copilot-instructions.md inside .github/
3. Open Copilot Chat (Ctrl+Alt+I)
4. Describe project: "Building a TypeScript Kanban board..."
5. Ask Copilot to generate custom instructions template
6. Add project-specific conventions and patterns
7. Request structure: "What directory structure do you recommend?"
8. Create folders manually: ProjectBoard/, .docs/
9. Generate tsconfig.json: Ask Copilot with specific prompt
10. Review & understand: Ask "Why this setting?"
11. Generate package.json: One file at a time
12. Test each step: Run tsc --version, verify configs
13. Refine if needed: "Add source maps for debugging"
```

**📌 Key Learning Points:**
- **Custom instructions first**: Set up .github/copilot-instructions.md before coding
- **Always-on context**: Instructions are included with EVERY Copilot interaction automatically
- **No repetition needed**: Set conventions once, Copilot remembers across all files
- **Copilot reads your instructions**: Better suggestions when context is clear
- **Build one piece at a time**: Understand each configuration before moving on
- **Ask "why" questions**: "Why use ES2020?" "Why strict mode?" - Copilot explains
- **Test incrementally**: Verify each config works before adding complexity
- **Iterate and refine**: Start basic, enhance with follow-up prompts
- **Learn from Copilot**: Study generated configs to understand best practices
- **Update instructions**: As patterns emerge, add them to copilot-instructions.md

### 1.3 Setup Development Environment with Copilot
- Install Live Server extension in VS Code
- Generate npm scripts for TypeScript compilation
- Configure TypeScript watch mode
- Set up Live Server extension settings (optional)

**Dev Server: VS Code Live Server Extension**

**Why Live Server Extension?**
- ✅ **No npm package needed** - Just a VS Code extension
- ✅ **One-click start** - "Go Live" button in status bar
- ✅ **Auto-reload** - Watches file changes automatically
- ✅ **Zero configuration** - Works out of the box
- ✅ **Beginner-friendly** - Visual interface, no command line
- ✅ **Latest version**: 5.7.9 (actively maintained)
- ✅ **14.94MB** - Lightweight extension

**Installation Steps:**
1. Open VS Code
2. Click Extensions icon (Ctrl+Shift+X)
3. Search for "Live Server" by Ritwick Dey
4. Click Install
5. Look for "Go Live" button in bottom-right status bar

**How to Use:**
1. Open `index.html` in VS Code
2. Right-click → "Open with Live Server" OR click "Go Live" button
3. Browser opens automatically at `http://127.0.0.1:5500`
4. Edit files → Browser auto-reloads on save

*This tutorial uses the **Live Server VS Code extension** for maximum simplicity - no npm packages, no configuration files, just one click!*

**🚨 Beginner Troubleshooting: Common Setup Issues**

**Problem: "node: command not found"**
- **Cause**: Node.js not installed or not in PATH
- **Solution**: 
  1. Download Node.js from [nodejs.org](https://nodejs.org/)
  2. Run installer (use default settings)
  3. Restart VS Code completely
  4. Open new terminal in VS Code
  5. Run `node --version` to verify

**Problem: "tsc: command not found"**
- **Cause**: TypeScript not installed yet
- **Solution**: This is normal! We'll install it with `npm install`
- **When**: After creating package.json in step 1.2

**Problem: Copilot not showing suggestions**
- **Cause**: Copilot not activated or no subscription
- **Solution**:
  1. Check Copilot icon in VS Code status bar (bottom right)
  2. Click icon → "Sign in to GitHub"
  3. Verify subscription at [github.com/settings/copilot](https://github.com/settings/copilot)
  4. Reload VS Code window (Ctrl+Shift+P → "Reload Window")

**Problem: "Permission denied" errors on npm install**
- **Cause**: Folder permissions (Windows/Mac/Linux)
- **Solution**:
  - Windows: Run VS Code as administrator (right-click → Run as administrator)
  - Mac/Linux: Don't use `sudo` with npm; fix permissions instead
  - See: [npm docs on permissions](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)

**Problem: Live Server doesn't auto-reload**
- **Cause**: Browser cache, file watching issue, or extension not running
- **Solution**:
  1. Check status bar: "Go Live" button should show "Port: 5500" when running
  2. Hard refresh browser (Ctrl+Shift+R or Cmd+Shift+R)
  3. Stop and restart: Click "Port: 5500" to stop, then "Go Live" to start again
  4. Check if files are saving: Look for dot (•) next to filename in VS Code
  5. Verify extension installed: Extensions panel → Search "Live Server" → Should show "Installed"
  6. Try different browser: Extension settings → Change CustomBrowser
  7. If still broken, ask Copilot: "Why isn't VS Code Live Server detecting file changes?"

✅ **Validation Checkpoint:**
Before moving to Phase 2, verify:
- [ ] `npm --version` shows version number
- [ ] `npx tsc --version` shows TypeScript version (5.9.3)
- [ ] VS Code shows Copilot suggestions when you type
- [ ] Live Server extension installed (check Extensions panel)
- [ ] "Go Live" button visible in VS Code status bar (bottom-right)
- [ ] Clicking "Go Live" opens browser at http://127.0.0.1:5500
- [ ] .github/copilot-instructions.md file exists and is not empty
- [ ] `npm run watch` compiles TypeScript without errors

**🤖 Copilot Techniques:**
- **Inline Suggestions**: Type `"scripts": {` and let Copilot suggest common scripts
- **Chat for Explanations**: Ask "What's the best setup for TypeScript hot reload?"
- **Multi-file Context**: Copilot reads package.json when suggesting scripts
- **Documentation Requests**: "Explain this tsconfig option in a comment"

**Example Prompts:**
```
"Create package.json for TypeScript 5.9 project with build and watch scripts"

"Generate npm scripts for: build TypeScript, watch mode (I'll use VS Code Live 
Server extension for serving)"

"Create tsconfig.json that outputs compiled JS to 'dist' folder for use with 
Live Server extension"

"How do I configure VS Code Live Server extension to work with TypeScript output?"
```

**📌 Key Learning Points:**
- **Ask for recommendations**: Copilot knows ecosystem best practices
- **Request alternatives**: "What are other options besides live-server?"
- **Get explanations**: Understanding tools helps you make better choices
- **Incremental setup**: One tool at a time, test before moving on

**Copilot-Generated package.json Scripts:**
```json
{
  "scripts": {
    "build": "tsc",
    "watch": "tsc --watch"
  },
  "devDependencies": {
    "typescript": "^5.9.3"
  }
}
```

**That's it! No dev server packages needed.**

**Development Workflow:**
1. Terminal: `npm run watch` (TypeScript compiles on file changes)
2. VS Code: Click "Go Live" button (serves files with auto-reload)
3. Edit TypeScript files → TypeScript compiles → Browser auto-reloads

**Optional: Live Server Extension Settings**

Create `.vscode/settings.json` in project root:
```json
{
  "liveServer.settings.port": 5500,
  "liveServer.settings.root": "/",
  "liveServer.settings.CustomBrowser": "chrome",
  "liveServer.settings.ignoreFiles": [
    ".vscode/**",
    "**/*.ts",
    "**/*.scss",
    "node_modules/**"
  ]
}
```

### 1.4 Create Documentation with Copilot
- Use Copilot to draft `vision.md` structure
- Generate `roadmap.md` template with project phases and tasks
- Create this tutorial outline with Copilot's help

**📦 Technology Stack Versions (November 2025)**

*These are the current stable versions used in this tutorial:*

| Technology | Version | Status | Notes |
|------------|---------|--------|-------|
| TypeScript | 5.9.3 | ✅ Latest | Released Oct 2024, fully stable |
| Bootstrap | 5.3.8 | ✅ Latest | Actively maintained |
| Node.js | 24.11.1 LTS | ✅ Recommended | Long-term support |
| Live Server (VS Code) | 5.7.9 | ✅ Latest | Extension by Ritwick Dey, 14.94MB |

**Why These Versions?**
- **TypeScript 5.9**: Latest stable with all modern features
- **Bootstrap 5.3**: Current major version, widely used
- **Node.js 24 LTS**: Long-term support, stable for production
- **Live Server Extension**: VS Code extension, zero config, beginner-friendly

**Updating in the Future:**
- TypeScript: Check [TypeScript releases](https://github.com/microsoft/TypeScript/releases)
- Bootstrap: Check [Bootstrap versions](https://getbootstrap.com/docs/versions/)
- Node.js: Check [Node.js releases](https://nodejs.org/en/about/releases/)
- Ask Copilot: "What are the latest stable versions of TypeScript, Bootstrap, and Node.js?"

**🎯 Special Note on Roadmap:**
The `roadmap.md` is the foundation of the project workflow. You'll:
1. Generate the roadmap with Copilot (organized by development phases)
2. Review and refine roadmap items
3. Convert roadmap items into tasks for each phase
4. Work through tasks one at a time
5. Review completion and update roadmap as you progress

This roadmap-to-task workflow demonstrates the Kanban system in practice while keeping development organized. We use a **single board** throughout to maintain focus on Copilot techniques.

**🤖 Copilot Techniques:**
- **Markdown Generation**: Copilot excels at structured documentation
- **Template Creation**: Ask for reusable document structures
- **Incremental Building**: Start with outline, expand sections one at a time
- **Context from Code**: With code files open, Copilot writes better docs

**Example Prompts:**
```
"Create an outline for a vision.md document for a Kanban board project"

"Expand the 'Architecture Overview' section with data flow explanation"

"Generate a roadmap.md template with sections for completed features and 
future enhancements. Structure it so roadmap items can become Kanban tasks"

"Create a roadmap with tasks organized by development phase: Setup, Data Layer, 
Core Logic, UI, Features. Each item should be actionable and trackable"

"Add a 'Design Decisions' section explaining why we chose JSON files over 
a database"
```

**Incremental Documentation Workflow:**
```
1. Start with structure: "Create outline for vision.md"
2. Review outline: Adjust sections as needed
3. Expand incrementally: "Expand the Architecture section"
4. Add specific content: "Explain why TypeScript strict mode"
5. Generate roadmap: "Create roadmap.md organized by phases"
6. Review roadmap: Ensure items are actionable and trackable
7. Refine with Copilot: "Make this section more beginner-friendly"
8. Cross-reference code: Keep TypeScript files open for context
9. Update as you build: Mark completed items, add learnings
```

**📌 Key Learning Points:**
- **Documentation grows with code**: Write docs as you build, not at the end
- **Roadmap drives development**: Structured workflow from roadmap → tasks → completion
- **One task at a time**: Complete and review each task before moving to next
- **Phase-based organization**: Group related work, review before moving to next phase
- **Single board workflow**: While multi-board capable, one board keeps tutorial focused
- **Copilot reads your code**: Better docs when related files are open
- **Incremental expansion**: Outline → sections → details
- **Teaching tool**: Writing docs with Copilot reinforces understanding
- **Living documentation**: Update roadmap as you complete phases

**Why Incremental Documentation Matters:**
- ✅ Reinforces what you learned in each phase
- ✅ Provides reference for future you
- ✅ Documents decisions while they're fresh
- ✅ Creates tutorial material naturally
- ✅ Roadmap becomes task backlog for the Kanban board
- ✅ Demonstrates the system with real project tasks
- ✅ Copilot learns your project better with each doc

---

[↑ Tutorial Home](../tutorial_outline.md) | [Next: Phase 2 →](./phase-02-data-layer.md)
