# Appendix A: Complete Troubleshooting Guide

[↑ Back to Tutorial Home](../tutorial_outline.md)

---

**Use this section when something goes wrong. Don't panic - every developer faces these issues!**

### Development Environment Issues

**Problem: "npm install fails with errors"**
- **Symptoms**: Red error messages, packages don't install
- **Common causes**:
  1. No internet connection → Check network
  2. npm registry timeout → Run `npm config set registry https://registry.npmjs.org/`
  3. Corrupted package-lock.json → Delete it and node_modules, run `npm install` again
  4. Permission issues → See "Permission denied" below
- **Fix**: Delete `node_modules` folder and `package-lock.json`, run `npm install` again
- **Ask Copilot**: "Why is npm install failing? Here's the error: [paste error]"

**Problem: "TypeScript won't compile"**
- **Symptoms**: `npm run build` fails with errors
- **Check**:
  1. Are there red squiggles in VS Code? Fix those first
  2. Run `npx tsc --noEmit` to see all TypeScript errors
  3. Verify TypeScript version: `npx tsc --version` (should show 5.9.3)
  4. Common fix: Missing types → `npm install --save-dev @types/node`
- **Beginner tip**: Read error messages carefully! TypeScript errors are descriptive
- **Version note**: This tutorial uses TypeScript 5.9.3 (latest stable as of Nov 2025)
- **Ask Copilot**: "Explain this TypeScript error: [paste error]"

**Problem: "Page shows blank screen"**
- **Symptoms**: Browser shows white screen, nothing renders
- **Debug steps**:
  1. Open DevTools (F12) → Console tab
  2. Look for red error messages
  3. Common errors:
     - "404 Not Found" → File path wrong, check src= paths
     - "SyntaxError: Unexpected token" → JSON syntax error
     - "Cannot read property of undefined" → Data not loaded yet
  4. Check Network tab → All files should show 200 status
- **Fix**: Error message tells you which file/line has the problem
- **Ask Copilot**: "Why is my page blank? Console shows: [paste error]"

### Data Loading Issues

**Problem: "boards.json not loading"**
- **Symptoms**: Console error "Failed to fetch boards.json"
- **Causes**:
  1. File path wrong → Check file is in correct location
  2. JSON syntax error → Validate at [jsonlint.com](https://jsonlint.com/)
  3. Server not serving JSON → Check Content-Type header in Network tab
- **Fix**: 
  **Ask Copilot for debugging code:**
  ```
  "Generate fetch debugging code that:
  1. Gets raw response text instead of parsing JSON
  2. Logs the raw content to console
  3. Catches and displays detailed error information
  
  This will help diagnose JSON fetch failures."
  ```
  
  Copilot generates diagnostic code to identify the exact problem.
  
- **Ask Copilot**: "JSON fetch failing, here's the error: [paste error]"

**Problem: "Tasks not appearing"**
- **Symptoms**: Board shows columns but no tasks
- **Debug checklist**:
  1. Check console for errors loading tasks JSON
  2. Verify tasks_main.json exists and has tasks array
  3. Check tasks have correct `boardId` matching current board
  4. Verify `status` matches a valid column ID
  5. Look in Network tab → tasks_main.json should show 200 status
- **Common cause**: Task `boardId` doesn't match board `id`
- **Fix**: Open tasks_main.json, verify all tasks have `"boardId": "main-board"`

### UI/Rendering Issues

**Problem: "Layout broken, elements overlapping"**
- **Symptoms**: Columns stack weirdly, cards overlap
- **Causes**:
  1. Bootstrap CSS didn't load → Check for 404 in Network tab
  2. CSS specificity conflict → Your styles override Bootstrap
  3. Flexbox/Grid mistake → Incorrect CSS properties
- **Fix**:
  1. Verify Bootstrap CDN link in HTML (check URL is correct)
  2. Hard refresh browser: Ctrl+Shift+R (Mac: Cmd+Shift+R)
  3. Check DevTools Elements tab → Inspect computed styles
- **Ask Copilot**: "My Kanban columns aren't displaying side-by-side, what's wrong?"

**Problem: "Times not updating"**
- **Symptoms**: Elapsed times stay frozen, don't increment
- **Debug**:
  1. Check if setInterval is running: Add `console.log('Update tick')` inside
  2. Verify tasks have `startedAt` timestamp
  3. Check console for errors in update function
- **Common cause**: Update function throwing error, stops interval
- **Fix**: Check console, fix the error, reload page
- **Ask Copilot**: "setInterval not running, here's my code: [paste code]"

### Browser/Performance Issues

**Problem: "Page slow with many tasks"**
- **Symptoms**: Laggy scrolling, slow rendering
- **Solutions**:
  1. Use DocumentFragment for batch rendering (see Phase 5)
  2. Reduce update frequency: Update every 60 seconds, not every second
  3. Limit rendered tasks: Show only first 20, "load more" button
  4. Check for memory leaks: DevTools → Memory → Take heap snapshots
- **Performance target**: <100ms render for 50 tasks
- **Ask Copilot**: "How can I optimize rendering performance for 100+ tasks?"

**Problem: "Browser DevTools closed accidentally"**
- **Fix**: Press F12 to reopen (Mac: Cmd+Option+I)
- **Tip**: Dock DevTools to side for easier development
  - Click ⋮ menu in DevTools → Dock side (right or left)

### Live Reload Issues

**Problem: "Changes not showing in browser"**
- **Symptoms**: Edit code, save, browser doesn't update
- **Try these fixes in order**:
  1. **Check file is saved**: VS Code shows • dot next to filename if unsaved (Ctrl+S to save)
  2. **Check TypeScript compiled**: If editing .ts files, check `npm run watch` is running and compiled successfully
  3. **Hard refresh browser**: Ctrl+Shift+R (bypasses cache)
  4. **Check Live Server running**: Status bar should show "Port: 5500" (not "Go Live")
  5. **Restart Live Server**: Click "Port: 5500" to stop, click "Go Live" to start
  6. **Check file is in workspace**: Live Server only watches files in opened VS Code workspace
  7. **Clear browser cache**: DevTools (F12) → Application → Clear storage
  8. **Check extension settings**: `.vscode/settings.json` may have `ignoreFiles` excluding your files
  9. **Try incognito/private window**: Rules out browser extension conflicts
- **TypeScript workflow**: Edit .ts → TypeScript compiles to .js → Live Server detects .js change → Browser reloads
- **Ask Copilot**: "VS Code Live Server not detecting file changes, what's wrong?"

### Git/Version Control Issues (If Using Git)

**Problem: "Git merge conflict in JSON files"**
- **Symptoms**: JSON files show conflict markers `<<<<<<< HEAD`
- **Fix for beginners**:
  1. Find conflict markers in file (search for `<<<<<<<`)
  2. Decide which version to keep (yours or theirs)
  3. Delete conflict markers and unwanted version
  4. Ensure JSON is still valid (use jsonlint.com)
  5. Save, add, commit
- **Prevention**: Communicate with team before editing same JSON files
- **Ask Copilot**: "How do I resolve JSON merge conflict?"

### When You're Completely Stuck

**Emergency Debugging Checklist:**
1. ✅ Check browser console (F12) → Any red errors?
2. ✅ Check VS Code Problems panel → Any TypeScript errors?
3. ✅ Is file saved? Look for • dot next to filename
4. ✅ Try hard refresh: Ctrl+Shift+R
5. ✅ Restart live-server: Ctrl+C, then `npm run dev`
6. ✅ Check JSON syntax: Paste into [jsonlint.com](https://jsonlint.com/)
7. ✅ Compare with working version: Did you break something since last working state?
8. ✅ Read error message completely: Often tells you exactly what's wrong
9. ✅ Ask Copilot: Paste error, describe what you were doing
10. ✅ Take a break: Fresh eyes often spot the issue immediately

**How to Ask for Help (Copilot or Humans):**
- ❌ "It doesn't work" → Too vague!
- ✅ "Board won't load. Console shows 'Cannot read boardId'. I was editing tasks_main.json when it broke."
- Include: What you were doing, what happened, what error you see
- Paste exact error messages (copy from console)
- Mention what you already tried

---

[↑ Back to Tutorial Home](../tutorial_outline.md)
