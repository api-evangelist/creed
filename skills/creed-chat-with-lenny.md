---
name: Chat with the Creed AI companion (Lenny)
description: Start or continue a conversation with Creed's AI Christian chatbot and read prior messages.
api: openapi/creed-openapi-original.json
operations:
  - chatbot_endpoint_api_chatbot_post
  - get_user_chats_api_chats_get
  - get_chat_messages_api_chats__chat_id__messages_get
  - get_chat_suggestions_api_chat_suggestions_get
---

# Chat with the Creed AI companion (Lenny)

Use the Creed API to hold a scripture-grounded conversation with the AI companion.

## Auth
- Send a Supabase-issued JWT in the `Authorization: Bearer <token>` header on every call.
- Many endpoints also expect an `x-user-id` header identifying the user.

## Steps
1. (Optional) Fetch conversation starters with `get_chat_suggestions_api_chat_suggestions_get`.
2. (Optional) List existing conversations with `get_user_chats_api_chats_get` to continue one.
3. Send a message with `chatbot_endpoint_api_chatbot_post`. Body fields include `message`, an
   optional `conversation_id` (omit to start a new chat), and `sendAudio` to request TTS audio.
4. Read the full thread with `get_chat_messages_api_chats__chat_id__messages_get` using the
   returned `chat_id`.

## Conventions & errors
- Pagination is offset/limit; error responses use the FastAPI `{"detail": ...}` envelope.
- 422 means a validation error — inspect `detail[].loc`/`detail[].msg`. See
  `conventions/creed-conventions.yml` and `errors/creed-problem-types.yml`.
- No idempotency-key contract; do not assume safe automatic retries of POSTs.
