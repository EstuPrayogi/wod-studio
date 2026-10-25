# WOD STUDIO Web Starter

Starter web app (dark mode) for Supabase. Includes email/password auth, coach class creation with an 8-character code, member join via code, workout publishing, member workout viewing, result logging and personal history.

## Configure on iPad
1. Download/extract this ZIP on a computer if possible. You can also use a code editor app that can edit local files on iPad.
2. Open `config.js`.
3. In Supabase Dashboard > Settings > API Keys, copy the Project URL from Integrations > Data API (the base URL, without `/rest/v1/`).
4. Copy the **Publishable key** beginning `sb_publishable_` from Settings > API Keys.
5. Paste both values into `config.js`. Never put a `secret` or `service_role` key in frontend code.
6. Host the folder on a static HTTPS host (for example, a static site host). Opening `index.html` as a local file may be blocked by browser module/network restrictions; use a local dev server or HTTPS hosting.

## Supabase database assumptions
This frontend expects the four tables and functions already created in the project:
- `classes`, `class_members`, `workouts`, `workout_results`
- RPC `create_class_with_code(p_name text)`
- RPC `join_class(p_code text, p_display_name text)`
- Supabase Auth email/password enabled

## Important security notes
- Do not consider this production-ready. Review all RLS policies before inviting real members.
- Current starter allows class owners to create/publish workouts under existing policies. Role management is not implemented: any authenticated account may be able to create a class, so this is not a coach-only system yet.
- A member leaderboard is intentionally not implemented because the current result RLS policies do not expose other members' results. Do not loosen result access policies just to build a leaderboard; implement a carefully scoped server-side view/RPC.
- Add rate limiting/abuse protection for class-code joins, email confirmation redirects, password reset, stronger coach role assignment, and production error handling before launch.
