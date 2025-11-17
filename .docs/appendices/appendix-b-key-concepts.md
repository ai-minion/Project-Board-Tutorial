# Appendix B: Key Concepts Explained

[↑ Back to Tutorial Home](../tutorial_outline.md)

---

### Why JSON Files Instead of a Database?

**Pros:**
- ✅ Zero setup - no database installation needed
- ✅ Version control friendly - Git can track changes
- ✅ Human readable - easy to debug and understand
- ✅ Simple CLI integration - standard file I/O
- ✅ Portable - works anywhere with file system
- ✅ Tutorial friendly - no complex backend setup

**Cons:**
- ❌ No concurrent write support
- ❌ Poor performance with large datasets (>1000 tasks)
- ❌ No built-in validation
- ❌ Manual reference integrity
- ❌ No transactions

**When to migrate to database:**
- Multiple users editing simultaneously
- More than 500 tasks per board
- Need for complex queries
- Audit trail requirements
- Production deployment

### Why Separate Task Files Per Board?

**Rationale:**
1. **Modularity** - Each board is self-contained
2. **Performance** - Only load tasks for active board
3. **Organization** - Easier to find and manage tasks
4. **CLI simplicity** - Clear which file to modify
5. **Scalability** - Can have different storage backends per board

**Alternative Considered:**
- Single tasks.json with all tasks
- Rejected because: harder to manage, slower to load, merge conflicts

### Why Activity Array Instead of Separate File?

**Rationale:**
1. **Atomicity** - Task and its history stay together
2. **Simplicity** - One data structure per task
3. **Performance** - No joins needed to display task
4. **Portability** - Easy to move task between boards

**Trade-off:**
- Activity can grow large (consider archiving old entries)

### Why Client-Side Rendering?

**Rationale:**
1. **Simplicity** - No server needed for tutorial
2. **Instant updates** - No round-trip for calculations
3. **Learning focus** - Teaches DOM manipulation
4. **Flexibility** - Easy to extend with interactions

**When to add server:**
- Need multi-user support
- Want to hide business logic
- Require authentication
- Need server-side validation

---

## Quick Reference: Time Estimates by Phase

| Phase | Topic                          | Duration | Cumulative |
|-------|--------------------------------|----------|------------|
| 1     | Project Setup                  | 30 min   | 30 min     |
| 2     | Data Layer Design              | 45 min   | 1h 15min   |
| 3     | Core Application Logic         | 60 min   | 2h 15min   |
| 4     | UI Foundation                  | 45 min   | 3h 00min   |
| 5     | Rendering Engine               | 60 min   | 4h 00min   |
| 6     | Interactive Features           | 45 min   | 4h 45min   |
| 7     | Enterprise Features            | 45 min   | 5h 30min   |
| 8     | Agent/CLI Integration (docs)   | 30 min   | 6h 00min   |
| 9     | Testing & Refinement           | 45 min   | 6h 45min   |
| 10    | Documentation                  | 30 min   | 7h 15min   |

**Total: ~7-8 hours** (focused development time)

---

## Learning Path Recommendations

### Beginner Path
**Prerequisites:** Basic HTML/CSS, JavaScript variables and functions

**Focus on:**
1. Phase 1-2: Understanding project structure and TypeScript types
2. Phase 4-5: HTML/CSS layout and basic rendering
3. Skip complex time calculations initially
4. Skip CLI integration documentation

**Expected time:** 4-5 hours

### Intermediate Path
**Prerequisites:** Comfortable with TypeScript, async/await, DOM manipulation

**Follow full tutorial:**
1. Complete all 10 phases in order
2. Implement all features
3. Review architecture decisions

**Expected time:** 6-8 hours

### Advanced Path
**Prerequisites:** Experienced with TypeScript, design patterns, testing

**Focus on:**
1. Quick implementation of basic features (Phases 1-6)
2. Deep dive into enterprise features (Phase 7)
3. Extend with testing framework
4. Implement 1-2 future enhancements
5. Add performance optimizations

**Expected time:** 8-12 hours (with extensions)

---

## Resources & References

### TypeScript (v5.9.3)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [What's New in TypeScript 5.9](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-9.html)
- [TypeScript Strict Mode](https://www.typescriptlang.org/tsconfig#strict)
- [Type Guards](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

### Bootstrap 5 (v5.3.8)
- [Bootstrap 5.3 Documentation](https://getbootstrap.com/docs/5.3/)
- [Bootstrap Cards](https://getbootstrap.com/docs/5.3/components/card/)
- [Bootstrap Grid System](https://getbootstrap.com/docs/5.3/layout/grid/)
- [Bootstrap Utilities](https://getbootstrap.com/docs/5.3/utilities/api/)

### Development Tools
- [Live Server Extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) (v5.7.9 - VS Code extension)
- [Node.js Documentation](https://nodejs.org/docs/latest-v24.x/api/) (LTS v24.11.1)
- [VS Code Extensions Guide](https://code.visualstudio.com/docs/editor/extension-marketplace)

### DOM & Web APIs
- [MDN: Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
- [MDN: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [MDN: localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

### Time & Dates
- [MDN: Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
- [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)
- [Intl.RelativeTimeFormat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/RelativeTimeFormat)

### Testing
- [Jest](https://jestjs.io/)
- [Playwright](https://playwright.dev/)
- [Testing Library](https://testing-library.com/)

### GitHub Copilot
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Custom Instructions Guide](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)
- [Copilot Best Practices](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot)
- [Copilot in VS Code](https://code.visualstudio.com/docs/copilot/overview)

---

[↑ Back to Tutorial Home](../tutorial_outline.md)
