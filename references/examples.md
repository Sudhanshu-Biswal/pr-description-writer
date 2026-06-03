# PR Description Examples

## Example 1 — Feature PR

**PR Title**
✨ feat(api): Add rate limiting to public API endpoints

**PR Description**
## What changed
Adds per-IP rate limiting to all public API routes to prevent abuse and reduce
infrastructure costs during traffic spikes.

## Changes breakdown
- `src/middleware/rateLimiter.ts` — New middleware implementing sliding window rate limiting
- `src/routes/api.ts` — Applies rateLimiter to all /api/public/* routes
- `tests/rateLimiter.test.ts` — Unit tests covering limit enforcement and Redis fallback

## How to test
1. Start the server: `npm run dev`
2. Hit any public endpoint 101 times in under 60 seconds
3. Confirm 429 response with Retry-After header on the 102nd request

## Breaking changes
None. Authenticated routes are unaffected.

## Related issues / links
Closes #234

---

## Example 2 — Bug Fix PR

**PR Title**
🐛 fix: Prevent null pointer crash on empty user profile load

**PR Description**
## What changed
Fixes a crash when a user with no profile data visited their settings page.
The component was reading user.profile.name without null checking user.profile first.

## Changes breakdown
- `src/components/UserProfile.tsx` — Added optional chaining and fallback default values

## How to test
1. Create a test account without completing profile setup
2. Navigate to /settings/profile
3. Confirm page loads without crashing and shows placeholder values

## Breaking changes
None.

## Related issues / links
Fixes #189

---

## Example 3 — Refactor PR

**PR Title**
♻️ refactor: Extract duplicated auth logic into shared middleware

**PR Description**
## What changed
Auth token validation was copy-pasted across 6 route files. Extracted into a
single auth.ts middleware, reducing duplication.

## Changes breakdown
- `src/middleware/auth.ts` — New shared auth middleware
- `src/routes/*.ts` — Replaced inline auth logic with authenticate middleware import

## How to test
1. Run existing test suite: `npm test` — all auth tests should pass
2. Make a request with an invalid token to any protected route
3. Confirm 401 Unauthorized is returned as before

## Breaking changes
None. All route behavior is identical.

## Related issues / links
Part of #201
