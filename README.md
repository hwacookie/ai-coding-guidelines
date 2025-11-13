# AI Coding Guidelines - Universal Best Practices

A centralized repository for universal AI coding guidelines and best practices that apply across all projects.

## 📚 Contents

- **UNIVERSAL_GUIDELINES.md** - Core guidelines covering:
  - Discussion-first principle
  - Communication best practices
  - Git safety rules
  - Feature branch workflow
  - Code organization
  - Testing practices
  - Common pitfalls

## 🎯 Purpose

Instead of duplicating guidelines across multiple project repositories, this central repo serves as the **single source of truth** for universal coding practices.

Each project's `.github/copilot-instructions.md` should reference this repository and extend it with project-specific rules.

## 🔗 How to Use in Projects

In your project's `.github/copilot-instructions.md`, add:

```markdown
## Universal Guidelines

For universal best practices that apply across all projects, see:
https://github.com/hwacookie/ai-coding-guidelines

Key universal rules:
- Never develop on main/production branches - use feature branches
- Always test locally before merging to main
- Never use git reset/revert without explicit approval
- Discuss major changes before implementing

### Project-Specific Guidelines

[Your project-specific rules here...]
```

## 📋 What Goes Where

### Universal Guidelines (This Repo)
- ✅ Feature branch workflow
- ✅ Git safety practices
- ✅ Communication principles
- ✅ Code organization patterns
- ✅ General best practices
- ✅ Common pitfalls

### Project-Specific Guidelines (Each Project's `.github/copilot-instructions.md`)
- ✅ Technology stack specifics (PHP, Python, Node.js, etc.)
- ✅ Project architecture details
- ✅ Deployment workflow
- ✅ Project-specific naming conventions
- ✅ Project structure and organization
- ✅ Custom development rules

## 🔄 Maintaining These Guidelines

- **Universal guidelines** are updated here when you discover better practices
- **Project-specific rules** are maintained in each project's repo
- **Always reference this repo** from project instructions
- **Keep in sync** - if a universal rule changes, projects will reference the updated version

## 📝 Version History

- **v1.0** (November 13, 2025) - Initial creation from coregames.de project guidelines

---

For questions or suggestions about these guidelines, check your individual project's documentation or update this file with improvements.
