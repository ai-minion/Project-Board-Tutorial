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
This is an enterprise Kanban board application with a hybrid architecture:
- **Frontend**: TypeScript, Bootstrap 5, vanilla JavaScript DOM manipulation
- **Backend**: Python for data management and CLI tools
- **Data Layer**: JSON files for persistence

Focus on clean, typed code with comprehensive documentation in both languages.

## Technology Stack
**Frontend:**
- TypeScript (strict mode enabled)
- Bootstrap 5.3.8 for UI components
- Vanilla JavaScript DOM manipulation
- Live Server extension for development

**Backend:**
- Python 3.8+ with type hints
- Standard library: json, pathlib, datetime
- board_manager.py module for data operations

**Data:**
- JSON files for data persistence
- Shared format between TypeScript and Python

## Coding Conventions

**TypeScript:**
- Use TypeScript strict mode (no `any` types)
- Prefer functional programming patterns
- Use `const` over `let` where possible
- All functions must have JSDoc comments
- Interfaces for all data structures

**Python:**
- Use type hints for all function parameters and returns
- Follow PEP 8 style guide
- Use pathlib for file operations (not os.path)
- Docstrings for all functions (Google style)
- Prefer dataclasses for structured data

**Shared:**
- Use semantic HTML5 elements
- Follow Bootstrap utility-first approach
- ISO 8601 timestamps in JSON
- Consistent naming across languages

## Architecture Patterns
- **Separation of concerns**: TypeScript handles UI, Python handles data
- **Frontend (TypeScript)**: Rendering, events, user interactions
- **Backend (Python)**: JSON file I/O, data validation, CLI tools
- **Pure functions**: For data transformations in both languages
- **Type safety**: TypeScript interfaces match Python type hints

## File Naming
- TypeScript: PascalCase for interfaces, camelCase for functions
- Python: snake_case for functions, PascalCase for classes
- JSON: lowercase with hyphens (boards.json, tasks_main.json)
- CSS: kebab-case for class names

## Preferences
- Prioritize code clarity over brevity
- Include error handling in all file operations
- Add accessibility attributes (ARIA) to interactive elements
- Generate comprehensive documentation (JSDoc for TypeScript, docstrings for Python)
- Use modern language features (ES2022 for TS, Python 3.8+ features)
```

**📌 Key Learning Points:**
- **Create before coding**: Set up instructions before generating code
- **Update as you build**: Refine instructions when patterns emerge
- **Be specific**: Detailed instructions = better suggestions
- **Include examples**: Show Copilot your preferred code style

### 1.2 Initialize Project Structure with Copilot

**Technology Stack (Latest Versions - November 2025):**

**Frontend:**
- **TypeScript**: 5.9.3 (latest stable)
- **Bootstrap**: 5.3.8 (latest stable)
- **Dev Server**: live-server extension for VS Code

**Backend:**
- **Python**: 3.8+ (3.12+ recommended for latest features)
- **Standard Library**: json, pathlib, datetime (no external packages required initially)

**Architecture:** TypeScript/JavaScript handles browser UI, Python handles data management through `board_manager.py`

**🤖 Copilot Techniques:**
- **Context Setting**: Open Copilot Chat and describe your project goals
- **Targeted Prompts**: Request one file/config at a time
- **File Generation**: Ask Copilot to create specific configuration files
- **Best Practices**: Request modern TypeScript AND Python configurations with explanations
- **Incremental Building**: Add complexity step-by-step, letting Copilot guide you

**Example Prompts:**
```
"What directory structure do you recommend for a hybrid TypeScript/Python 
Kanban board with separate frontend and backend?"

"Create a tsconfig.json for a TypeScript 5.9 project that compiles to ES2022 
with strict mode enabled, outputting to a dist folder"

"Generate a Python requirements.txt for a project that only uses standard 
library modules (json, pathlib, datetime) - should it be empty?"

"Create a .gitignore file for a TypeScript + Python project"
```

**Project Structure:**
```
ProjectBoard/
├── .github/
│   └── copilot-instructions.md    # Copilot context (both TS & Python)
├── .docs/                          # Tutorial documentation
├── ProjectBoard/                   # Application code
│   ├── html/                       # HTML files
│   ├── css/                        # Stylesheets
│   ├── js/                         # TypeScript/JavaScript (frontend)
│   ├── data/                       # JSON data files
│   └── board_manager.py            # Python backend module
├── tsconfig.json                   # TypeScript configuration
├── .gitignore                      # Git ignore patterns
└── README.md                       # Project documentation
```

**Incremental Workflow:**
```
1. Create .github directory in project root
2. Create copilot-instructions.md inside .github/
3. Open Copilot Chat (Ctrl+Alt+I)
4. Describe project: "Building a TypeScript frontend + Python backend Kanban board..."
5. Ask Copilot to generate custom instructions template for both languages
6. Add project-specific conventions for TypeScript AND Python
7. Request structure: "What directory structure do you recommend?"
8. Create folders: ProjectBoard/ (with html/, css/, js/, data/ subfolders), .docs/
9. Create board_manager.py in ProjectBoard/
10. Generate tsconfig.json: Ask Copilot with specific prompt
11. Set up Python environment (see section 1.2.5 below)
12. Review & understand: Ask "Why this setting?"
13. Test each step: Run tsc --version, python --version, verify configs
14. Refine if needed: "Add source maps for debugging"
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

### 1.2.5 Python Environment Setup with Copilot

**Why Python for This Project?**
- **Backend data management**: Read/write JSON files safely
- **CLI tools**: Command-line task management
- **Data validation**: Ensure JSON integrity before saving
- **Type hints**: Modern Python type annotations similar to TypeScript

**🤖 Copilot Techniques:**
- **Virtual Environment**: Ask Copilot about venv best practices
- **Module Structure**: Get guidance on Python project organization
- **Type Hints**: Copilot adds modern type annotations automatically

**Example Prompts:**
```
"Should I create a virtual environment for a simple Python project that 
only uses standard library? What are the pros and cons?"

"Create a board_manager.py module with functions to load and save JSON 
files using pathlib and the json module. Include type hints."

"What Python version should I target for modern type hints and pathlib 
support? What's the minimum version?"
```

**Python Setup Steps:**

**1. Verify Python Installation:**
```bash
python --version  # Should show 3.8 or higher
```

**2. Decide on Virtual Environment (Optional for this project):**

Ask Copilot:
```
"For a project using only Python standard library (json, pathlib, datetime), 
do I need a virtual environment or can I use the system Python?"
```

**Copilot's typical advice:**
- ✅ **Use venv if**: You plan to add packages later (pytest, requests, etc.)
- ✅ **Skip venv if**: Only using standard library and want simplicity
- ✅ **Best practice**: Create venv anyway for isolation

**3. Create Virtual Environment (Recommended):**

**Windows:**
```powershell
# In project root
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
# In project root
python3 -m venv venv
source venv/bin/activate
```

**Verify activation:**
```bash
python --version  # Should still show Python 3.8+
which python      # macOS/Linux: should point to venv
where python      # Windows: should show venv path first
```

**4. Create requirements.txt:**

For now, it's empty (using standard library only):
```txt
# requirements.txt
# Using Python standard library only
# Future: add pytest, click, pydantic if needed
```

Ask Copilot:
```
"Create a requirements.txt file for a Python project using only standard 
library. What should I include? Should it list standard modules?"
```

**5. Update .gitignore for Python:**

Ask Copilot to add Python patterns:
```
"Add Python-specific patterns to .gitignore: venv, __pycache__, .pyc files"
```

Copilot will suggest:
```gitignore
# Python
venv/
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
```

**📌 Key Learning Points:**
- **Python 3.8+ minimum**: Required for modern type hints and pathlib
- **Virtual environment optional**: Not required for standard library only
- **Type hints are free**: No installation needed, built into Python 3.5+
- **Standard library is powerful**: json, pathlib, datetime handle most needs
- **Activate venv in terminal**: Must activate before running Python commands

**Beginner Concept: What is a Virtual Environment?**

Ask Copilot:
```
"Explain Python virtual environments to a beginner. Why use them? 
How do they differ from the system Python?"
```

**Simple explanation:**
- **Virtual environment**: Isolated Python installation for your project
- **Why use it**: Prevents package conflicts between projects
- **When to skip**: If only using standard library (like our project initially)
- **When required**: When installing packages with pip

**Python Project Checklist:**
- [ ] Python 3.8+ installed (`python --version`)
- [ ] Virtual environment created (optional but recommended)
- [ ] venv activated (if created)
- [ ] board_manager.py file created in ProjectBoard/
- [ ] .gitignore includes Python patterns
- [ ] Understand: TypeScript = frontend, Python = backend

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

**Problem: "python: command not found" or "python3: command not found"**
- **Cause**: Python not installed or not in PATH
- **Solution**:
  1. Download Python from [python.org](https://www.python.org/downloads/)
  2. Run installer - **CHECK "Add Python to PATH"** during installation
  3. Restart VS Code completely
  4. Open new terminal in VS Code
  5. Try both `python --version` and `python3 --version`

**Problem: "node: command not found"** (if using TypeScript compilation)
- **Cause**: Node.js not installed or not in PATH (TypeScript compiler runs on Node)
- **Solution**: 
  1. Download Node.js from [nodejs.org](https://nodejs.org/)
  2. Run installer (use default settings)
  3. Restart VS Code completely
  4. Open new terminal in VS Code
  5. Run `node --version` to verify

**Problem: "tsc: command not found"**
- **Cause**: TypeScript not installed yet
- **Solution**: Install TypeScript globally: `npm install -g typescript`
- **Verify**: `tsc --version`

**Problem: Virtual environment not activating**
- **Windows**: Use `venv\Scripts\activate` (backslashes)
- **macOS/Linux**: Use `source venv/bin/activate` (forward slashes)
- **PowerShell**: May need to run: `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`

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
