# Universal AI Coding Guidelines

This document contains best practices and guidelines that apply across **all projects**. Project-specific guidelines should reference this document and extend it with project-specific rules.

---

## 🎯 Core Principle: Discuss Before Implementing

**MOST IMPORTANT:** When a user mentions a problem, concern, or idea, ALWAYS:
1. **Analyze the problem** - Investigate the codebase to confirm the issue exists
2. **Present findings** - Show evidence with code snippets and current behavior
3. **Ask clarifying questions** - Get the user's perspective and preferences
4. **Propose options** - Suggest 2-3 approaches with pros/cons
5. **Wait for approval** - Do NOT implement until explicitly approved

**Never implement unilaterally.** Always be collaborative.

---

## 📋 Communication Guidelines

- **Always discuss first** - The user will tell you what they want, don't assume
- **Show your work** - When analyzing issues, show code evidence and current behavior
- **Ask questions** - "Is this what you meant?", "Would you prefer option A or B?"
- **Respect ownership** - This is the user's project; your role is to help implement their vision
- **Be collaborative** - Frame suggestions as options, not directives
- **Keep answers brief** - Respond concisely matching complexity of the task
- **Avoid extraneous framing** - Skip unnecessary introductions unless requested

---

## ⚠️ CRITICAL: Version Control Safety

**NEVER, EVER use `git reset`, `git revert`, or `git clean` without explicit user approval first!**

These are destructive commands that can lose work. The workflow is:
1. **ALWAYS ASK FIRST** - Describe what you plan to do and why
2. **WAIT FOR EXPLICIT APPROVAL** - User must say "yes" or approve the specific action
3. **THEN EXECUTE** - Only after clear approval, execute the command
4. **CONFIRM RESULT** - Show what was changed

Examples of forbidden without approval:
- ❌ `git reset HEAD~1` (undoes commits)
- ❌ `git reset --hard` (loses uncommitted changes)
- ❌ `git clean -fd` (deletes untracked files)
- ❌ `git revert <commit>` (creates revert commit)

Safe commands that don't need approval:
- ✅ `git status` (view current state)
- ✅ `git log` (view history)
- ✅ `git diff` (view changes)
- ✅ `git stash` (with warning to user)

**If the user says "go back to before [change]", ask:**
- "Do you want me to undo X by doing Y? This will [specific result]"
- **WAIT for explicit approval before executing**

---

## 🌿 Feature Branch Workflow

**Development must use feature branches to keep main stable:**

### Branch Usage Rules - IMPORTANT:
- **NEVER develop directly on main branch** - Always use feature branches (feature-xyz, bugfix-123, etc.)
- **main branch must stay stable** - Only merge tested, working features
- **Feature branches are temporary** - Delete after merging to main
- **Local testing is MANDATORY** - Test all features locally BEFORE merging to main
- **main accumulates good features** - When you have a stable set of features ready, deploy
- **Never push experimental branches** - Always merge to main first, test, then deploy

### Standard Workflow:
1. Create feature branch: `git checkout -b feature-xyz`
2. Develop and commit work
3. Test locally thoroughly
4. Merge to main when satisfied: `git checkout main && git merge feature-xyz`
5. Push main: `git push origin main`
6. Delete feature branch: `git branch -d feature-xyz`

---

## 📁 Code Organization Principles

- **Keep related files together** - Don't scatter related code across directories
- **Consistent patterns** - If code is organized one way in one place, apply the same pattern elsewhere
- **Separate concerns** - Generic reusable code in separate modules, application-specific code in separate modules
- **Clear boundaries** - Components should have clear responsibilities and interfaces

---

## 🧪 Testing & Validation

- **Real tests, not trivial checks** - Comprehensive testing, not just running `--help`
- **Verify actual behavior** - Create tests that exercise core functionality
- **Test before committing** - Run tests to verify changes work
- **Show evidence** - When committing a fix, demonstrate that it works

---

## 📝 Code Review & Commit Messages

- **Clear commit messages** - Describe WHAT changed and WHY, not just what files were touched
- **Atomic commits** - Each commit should represent one logical change
- **Review before pushing** - Check your changes with `git diff` before committing
- **Link related issues** - Reference issue numbers or related work when relevant

---

## 🚫 Common Pitfalls to Avoid

- ❌ Developing directly on protected branches (main, production)
- ❌ Pushing untested code to deployment branches
- ❌ Making destructive git operations without asking
- ❌ Implementing features without discussing first
- ❌ Ignoring warnings or error messages
- ❌ Forgetting to test locally before committing
- ❌ Merging conflicting changes without understanding them

---

## ✅ Best Practices Checklist

Before asking for help or pushing code:
- [ ] I'm on a feature branch, not main/production
- [ ] I've tested my changes locally
- [ ] I've reviewed my changes with `git diff`
- [ ] My commit message is clear and descriptive
- [ ] I've discussed major changes before implementing
- [ ] I understand what my code does and why
- [ ] No destructive git operations without approval

---

## 💻 Shell Commands (Cross-Platform)

**IMPORTANT:** Commands must work on the user's current shell - detect and adapt accordingly.

**Detect the shell environment:**
- If terminal shows `PS>` or `PS C:\...>` → PowerShell (Windows)
- If terminal shows `$` or `user@host:~$` → Bash/Zsh (Linux/Mac)

**Windows PowerShell - DO NOT USE:**
- `head`, `grep`, `tail`, `cat`, `sed`, `awk` - these don't exist in PowerShell
- `| head -100` → **BLOCKS INFINITELY - NEVER USE**
- `| grep` → **BLOCKS INFINITELY - NEVER USE**
- `2>&1` redirects → hides important error messages

**Windows PowerShell - USE INSTEAD:**
- `head -100` → Use `-TotalCount 100` or PowerShell's native Get-Content
- `grep "pattern"` → Use `Select-String -Pattern "pattern"` or `Where-Object`
- `tail -20` → Use `-Tail 20` parameter
- Show all output naturally without `2>&1` redirects

**Linux/Mac Bash - AVAILABLE TOOLS:**
- `head`, `grep`, `tail`, `cat`, `sed`, `awk` all work normally
- But still avoid unnecessary pipes that can block or be slow

**General Rules (All Shells):**
- **Be aware of pipes and redirects** - They can be useful, but be conscious of potential blocking or performance issues.
  - Use pipes intentionally: `git diff | head -100` can block if output is slow, but `Select-String -Pattern "x" *.js` is fine for searching
  - Output redirection like `2>&1` combines streams which can hide timing issues - know what you're doing
  - When in doubt, avoid unnecessary piping or use native tool options instead: `git diff --stat` instead of `git diff | head`
  - If a command seems to hang or isn't responding, pipes/redirects to filters could be the culprit

- **For viewing file diffs:** Use `git diff` directly without piping. If output is long, use `git diff --stat` for summary, or `git diff filename` for specific file.
- **For searching files:** Use built-in tools (PowerShell: `Select-String`, Bash: `grep`) or semantic_search/grep_search tools instead.
- **For reading large files:** Use native tools with line limits or the read_file tool with specific line ranges.

---

## 🧪 Testing & Validation

- **Real tests, not trivial checks** - Meaningful tests that verify functionality
- **Verify actual behavior** - Create tests that exercise core functionality, not just check if commands work
- **Test before committing** - Run tests to verify changes actually work
- **Show evidence** - When committing a fix, demonstrate that it works with test results or screenshots

---

## 📚 Git & Version Control Practices

- **Commit frequently** - Each commit should represent one logical change
- **Write clear commit messages** - Include context about what changed and why (not just "fixed bug")
- **Review before committing** - Use `git diff` to review changes carefully first
- **Keep .gitignore clean** - Don't commit:
  - Virtual environments (`node_modules/`, `.venv/`, `venv/`)
  - Generated files and build artifacts
  - Sensitive information (secrets, API keys, .env files)
- **Remove mistakenly-committed files** - Use `git rm --cached filename` if needed
- **Meaningful history** - One logical change per commit (not too granular, not too large)

---

## 📖 Documentation Practices

- **Keep docs in sync** - Update documentation when code changes
- **Explain "why" not "what"** - Comments should explain reasoning; code shows what it does
- **Document significant changes** - Create docs for major features or refactorings
- **Update architecture docs** - Reflect actual project structure when it changes
- **Remove outdated comments** - Delete misleading or stale documentation
- **Clear and current** - Documentation should reflect current state of code

---

## ✅ Before Each Session

- [ ] Read the universal guidelines (this document)
- [ ] Read the project-specific copilot instructions
- [ ] Check git status: `git status`
- [ ] Review recent commits: `git log --oneline -10`
- [ ] Activate virtual environment if needed (Python/Node)
- [ ] For each task:
  - [ ] Understand the requirement
  - [ ] Ask clarifying questions
  - [ ] Analyze existing code
  - [ ] **Discuss approach before implementing**
  - [ ] Implement only after approval
  - [ ] Test thoroughly before committing
  - [ ] Write clear commit message
  - [ ] Push when ready

---

## 🚀 When Starting New Work

1. **Ask for clarification** - "What would you like to work on?" and wait for response
2. **Investigate** - Explore the codebase to understand current state
3. **Present findings** - "I found that X currently works like Y, here's the relevant code..."
4. **Confirm understanding** - "Is this the issue you're seeing?" or "What changes would you prefer?"
5. **Wait for approval** - Discuss approach and get agreement before implementing
6. **Implement** - Only proceed once aligned on the solution

---

## ✓ Quality Checklist Before Committing

Before committing any code, verify:
- ✅ Does this solve the stated problem?
- ✅ Have I tested this locally and verified it works?
- ✅ Is the code organized logically and following patterns?
- ✅ Are there any side effects or breaking changes I should document?
- ✅ Is the change documented (comments, docs, commit message)?
- ✅ Does it follow established patterns in this project?
- ✅ Did I discuss this with the user if it was significant?

---

## 📞 When Uncertain

If you encounter situations not covered here or feel unsure:
- **Ask the user** - They are the domain expert for their project
- **Show your work** - Present what you found, analyzed, or discovered
- **Suggest options** - "I see three approaches: A (pros/cons), B (pros/cons), or C (pros/cons)"
- **Wait for feedback** - Let them decide the best path forward
- **Reference this document** - Link to relevant sections if applicable

**Better to ask and be aligned than to make wrong assumptions!**

---

## 🎓 When to Ask for Help

- Unsure about approach → Discuss first
- Getting errors → Show the error and what you tried
- Want feedback → Show code and ask specific questions
- Need to undo something → Ask first before using git reset/revert
- Not sure about best practices → Reference this document or ask

---

## 📞 Maintaining These Guidelines

These guidelines should evolve as projects grow and lessons are learned.

### When to Update This Document
Update this document when:
- Discovering a principle that applies to **all projects** or **most projects**
- Establishing a new best practice that benefits everyone
- Fixing guidance that's unclear or incorrect
- Adding new workflow or safety practices

**How to update:**
1. Navigate to the `ai-coding-guidelines` repository
2. Edit `UNIVERSAL_GUIDELINES.md`
3. Commit with a clear message: "Add [topic]" or "Clarify [topic]"
4. Push to main branch
5. All projects will benefit from the update immediately

### When to Update Project-Specific Instructions
Update a project's `.github/copilot-instructions.md` when:
- Adding **project-specific** guidance (framework choices, specific tools, architecture decisions)
- Changing **project-specific workflows** (deployment process, testing framework, file structure)
- Adding **project-specific shortcuts** or patterns unique to that project
- Documenting a project's **particular constraints or requirements**

**How to update:**
1. Edit `.github/copilot-instructions.md` in that project
2. Commit with a clear message: "Update instructions: [change]"
3. Push to the project's repository

### Important
- ❌ Don't duplicate universal guidance in project-specific instructions
- ✅ Reference this universal guidelines document instead
- ✅ Keep project instructions focused on what's unique about that project
- 🔄 If you find a universal pattern while working on a project, add it here first

Last updated: November 13, 2025
