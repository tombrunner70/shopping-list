---
name: auto-code-review
description: Automatically review code you just wrote or changed. Use after finishing any code edit, before reporting a task as done, or when the user asks to review, check, or audit code. Covers correctness bugs, security, error handling, readability, and tests.
---

# Auto Code Review

Review the code that was just changed, then report findings. Do not rewrite code unless the user asks.

## 1. Find what changed
- If this is a git repo, run `git diff` (and `git diff --staged`) to get the changes.
- Otherwise, review the files you edited in this session.
- Read each changed file in full where needed, not just the diff, so you understand the surrounding context.

## 2. Check each change against this checklist
1. **Correctness**: logic errors, off-by-one, null/undefined handling, wrong conditions, unhandled edge cases, race conditions.
2. **Security**: injection (SQL, shell, HTML/XSS), hard-coded secrets, unsafe deserialization, missing input validation, path traversal.
3. **Error handling**: swallowed exceptions, missing failure paths, unclear error messages, resources not released.
4. **Readability**: unclear names, overly long functions, duplicated logic, dead code, misleading comments.
5. **Performance**: unnecessary loops or queries, repeated work, blocking calls in hot paths.
6. **Tests**: new behavior without tests, tests that don't assert anything meaningful.

## 3. Verify before reporting
- Only report issues you can point to in the code. Cite `file_path:line_number`.
- If unsure, say it is a possible issue and explain what you could not confirm.
- Run the project's tests or linter if they exist and are quick; report real failures.

## 4. Report format
Group findings by severity, most severe first:

- **Critical**: bug or vulnerability that breaks behavior or security
- **Warning**: likely problem or risky pattern
- **Suggestion**: readability or maintainability improvement

For each finding give: location, what is wrong, why it matters, and a concrete fix.

End with a one-line verdict: `Ready to merge`, `Needs changes`, or `Blocked`. If nothing was found, say so plainly and list what you checked.
