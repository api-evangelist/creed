---
name: Generate and listen to a daily prayer
description: Generate a personalized daily prayer, fetch its audio, and pull topical prayers from the library.
api: openapi/creed-openapi-original.json
operations:
  - generate_daily_prayer_api_daily_prayer_post
  - get_daily_prayer_audio_api_daily_prayer_audio_get
  - get_library_prayer_api_prayer_library__topic__get
---

# Generate and listen to a daily prayer

Produce a personalized daily prayer and optionally its narrated audio.

## Auth
- `Authorization: Bearer <Supabase JWT>` on every call; include `x-user-id` where required.

## Steps
1. Generate the prayer with `generate_daily_prayer_api_daily_prayer_post`.
2. Retrieve narrated audio with `get_daily_prayer_audio_api_daily_prayer_audio_get`.
3. For a topical prayer instead of a generated one, call
   `get_library_prayer_api_prayer_library__topic__get` with the desired `topic` path value; a
   `lang` query parameter selects the language.

## Conventions & errors
- FastAPI `{"detail": ...}` error envelope; 422 = validation error (see `errors/creed-problem-types.yml`).
- No idempotency contract — see `conventions/creed-conventions.yml`.
