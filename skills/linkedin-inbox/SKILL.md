---
name: linkedin-inbox
description: Use when the user wants to check their LinkedIn inbox, read LinkedIn messages or conversations, find unread messages or replies they owe, and draft responses. Send replies only with user approval. This skill handles LinkedIn messaging, not email inboxes.
---

# LinkedIn inbox

Read [account access and limits](../../references/account-and-limits.md) before using tools.

## Find conversations needing attention

Use `linkedin_list_chats` and follow `next_cursor` within the requested scope. Start with `unread: true` for unread-message triage. For conversations waiting for a reply, also inspect recent conversations without the unread filter. A read conversation can still need a reply.

Use `linkedin_get_messages` for relevant `chat_id` values. Messages arrive most recent first. Check who sent the latest message and interpret the exchange in chronological order. An unread count or chat snippet alone does not prove that the user owes a reply.

Present the person or conversation name, the latest inbound request, its timestamp, and a suggested next action. State the number of conversations inspected and whether more pages remain. Do not claim to have checked the entire inbox after one page. Attachment metadata does not reveal attachment contents.

## Draft and send replies

Draft replies using the conversation's facts and the user's requested tone. Keep commitments, dates, and claims grounded in the conversation or the user's instructions.

Show the recipient and exact text before calling `linkedin_send_message` with `chat_id` and `text`. Send only after the user authorizes that reply. If they already approved that exact draft, proceed without another approval request.

Confirm success from the tool result. If the outcome is uncertain, inspect the conversation with a fresh read before retrying. Reading or summarizing does not authorize `linkedin_mark_read`; use it when the user asks to mark the conversation read or unread.

For several approved replies, use [LinkedIn outreach](../linkedin-outreach/SKILL.md) to schedule the batch.
