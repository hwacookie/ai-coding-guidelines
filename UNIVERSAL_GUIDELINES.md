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

## 🎓 When to Ask for Help

- Unsure about approach → Discuss first
- Getting errors → Show the error and what you tried
- Want feedback → Show code and ask specific questions
- Need to undo something → Ask first before using git reset/revert
- Not sure about best practices → Reference this document or ask

---

## 📞 Questions or Updates

These guidelines should evolve as projects grow and lessons are learned. If you discover a gap or want to add something, update this document and commit it to the repository.

Last updated: November 13, 2025
