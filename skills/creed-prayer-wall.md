---
name: Submit and browse the prayer wall
description: Submit a prayer request to the moderated prayer wall, browse current prayers, and comment.
api: openapi/creed-openapi-original.json
operations:
  - submit_prayer_api_prayer_wall_post
  - get_current_prayers_api_prayer_wall_get
  - get_prayer_by_id_api_prayer_wall__prayer_id__get
  - submit_comment_api_prayer_wall__prayer_id__comments_post
---

# Submit and browse the prayer wall

Post a prayer request to Creed's community prayer wall and engage with others' prayers.

## Auth
- `Authorization: Bearer <Supabase JWT>` on every call; include `x-user-id` where required.

## Steps
1. Submit a prayer with `submit_prayer_api_prayer_wall_post`. The wall is moderated — a submission
   may be pending approval before it appears publicly.
2. Browse current prayers with `get_current_prayers_api_prayer_wall_get`.
3. Read a single prayer with `get_prayer_by_id_api_prayer_wall__prayer_id__get` using its `prayer_id`.
4. Add a comment with `submit_comment_api_prayer_wall__prayer_id__comments_post`.

## Conventions & errors
- Offset/limit pagination on listing endpoints; FastAPI `{"detail": ...}` error envelope.
- 403 = not authorized; 404 = prayer not found. See `errors/creed-problem-types.yml`.
- No idempotency contract; avoid blind POST retries — see `conventions/creed-conventions.yml`.
