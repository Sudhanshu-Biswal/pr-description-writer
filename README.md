# pr-description-writer

A Claude Code skill that writes your pull request descriptions for you — from diff to markdown in seconds.

Writing a good PR description takes time. You have to remember what changed, why it changed, and how someone else should verify it. Most people either skip it or write something vague. Reviewers suffer.

This skill reads your actual git diff and does the writing for you.

---

## What it does

Run `/pr-description-writer` in any git repository. Claude will:

1. Read your `git diff`, commit messages, and changed files
2. Auto-detect the PR type (feature, bug fix, refactor, etc.)
3. Generate a clean PR title with the right emoji prefix
4. Write a complete 6-section description — ready to paste into GitHub

---

## Output example

**PR Title**
✨ feat(api): Add rate limiting to public API endpoints (#234)
**PR Description**
```markdown
## What changed
Adds per-IP rate limiting to all public API routes to prevent abuse and
reduce infrastructure costs during traffic spikes.

## Changes breakdown
- `src/middleware/rateLimiter.ts` — New sliding window rate limiting middleware
- `src/routes/api.ts` — Applies rateLimiter to all /api/public/* routes
- `tests/rateLimiter.test.ts` — Unit tests covering enforcement and Redis fallback

## How to test
1. Start the server: `npm run dev`
2. Hit any public endpoint 101 times in under 60 seconds
3. Confirm 429 response with `Retry-After` header on the 102nd request

## Screenshots / output
HTTP/1.1 429 Too Many Requests
{ "error": "Rate limit exceeded. Try again in 42 seconds." }

## Breaking changes
None. Authenticated routes are unaffected.

## Related issues / links
Closes #234
```

---

## Install

```bash
git clone https://github.com/Sudhanshu-Biswal/pr-description-writer ~/.claude/skills/pr-description-writer
```

Then reload skills in Claude Code.

---

## Usage
/pr-description-writer
No arguments. No configuration. Works on any git repo — Node, Python, Go, Rust, monorepos.

---

## File structure
pr-description-writer/
├── SKILL.md
├── README.md
├── LICENSE
├── pr-description-writer.skill
└── references/
    ├── conventional-commits.md  
    └── examples.md              
---

## Why this exists

PR descriptions are communication, not ceremony. A good one tells the reviewer what changed, why it matters, and how to verify it — without them having to read every line of diff.

This skill exists because that communication shouldn't require extra effort after the code is already written.
