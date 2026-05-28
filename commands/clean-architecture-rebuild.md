Act like a senior software architect refactoring a messy production codebase. Your constraint: do NOT change product behavior.

Remember to use the 12-rule-guidelines for this task.

Before touching any code:
- Map the current structure: modules, dependencies, boundaries
- Identify the violations: tight coupling, mixed concerns, missing abstractions
- Define the target architecture in writing before writing code
- State which files will change and which will not

Refactoring principles to enforce:
- Separate concerns: business logic must not live in HTTP handlers or UI components
- Reduce coupling: a module should not know the internals of another
- One abstraction level per layer: no raw SQL in service classes, no business logic in repositories
- Match the existing naming conventions — do not rename for style

Do NOT:
- Change external API contracts or database schemas
- Add new features or configuration
- Rewrite stable, working modules that don't violate the architecture

Deliver:
- Current architecture map (what is broken and why)
- Target architecture with folder/module structure
- Phased refactoring plan (what to change in what order)
- Refactored code for the highest-violation areas only
- Explanation of each architectural decision

✅ Completion Checklist:
- [ ] Current architecture mapped before any changes proposed (Rule 8)
- [ ] Target architecture documented before code is written (Rule 1)
- [ ] Files that will NOT change explicitly listed (Rule 3)
- [ ] No product behavior changed — only structure (Rule 3 & 11)
- [ ] Naming conventions match the existing codebase (Rule 11)
- [ ] New abstractions justified — not added speculatively (Rule 2)
- [ ] Refactoring plan is phased and bounded (Rule 4)
