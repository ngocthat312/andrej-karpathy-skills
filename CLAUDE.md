# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.
## Project-Specific Guidelines
- Also follow project-specific guidelines by reading the project's README.md, AGENTS.md,..
- Read in the folder "/sop" to explain the business context of the EMM platform across ingestion, metadata, authoring, review, the tickets and publishing workflows. It is designed for onboarding, product alignment, and delivery planning before implementation details.
- For EMM, prioritize stability and maintainability over speed. Avoid speculative features or optimizations. Focus on clear, simple code that meets the requirements without overengineering.
- For EMM, when making changes, only modify the files and lines necessary to implement the requested feature or fix.
Don't refactor unrelated code or change formatting unless it directly supports the task. This minimizes risk and keeps diffs focused.
- Use Info Log. We should always be aware of requests coming into and going out of the system.
- Use Error Log. We should log all errors in the system, including validation errors, exceptions, and failed operations.
This will help us identify and troubleshoot issues quickly.
- For EMM, when implementing new features, write tests that cover the expected behavior and edge cases. This ensures that the feature works as intended and helps prevent regressions in the future.
- For EMM, when fixing bugs, first write a test that reproduces the issue. Then implement the fix and verify that the test passes. This ensures that the bug is properly addressed and prevents it from recurring.
- For EMM, when refactoring code, ensure that all existing tests pass before and after the changes. This confirms that the refactor did not introduce any regressions and maintains the integrity of the codebase.
