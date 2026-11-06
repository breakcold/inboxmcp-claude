---
name: inbox
description: Use when the user wants to check messages across LinkedIn, WhatsApp, Telegram, Instagram, or Facebook Messenger, find unread conversations or replies they owe on any of these networks, read a conversation, draft replies, start a conversation, or mark chats read. Send only with user approval. This skill handles these networks' direct messages, not email.
---

# Inbox across networks

Read [account access and limits](../../references/account-and-limits.md) before using tools.

## Find conversations needing attention

Call `inbox_list_chats` to list conversations from every connected account, most recent first. Pass `provider` to stay on one network, or `account` for one account. Start with `unread: true` for unread triage. For replies the user owes, also inspect recent conversations without the unread filter. A read conversation can still need a reply.

Each item has `chat_id`, `account_id`, `provider`, and `person_id` for one-to-one chats. On Facebook, this covers the personal Messenger inbox only: the inboxes of the user's Pages and message requests are listed with the [Facebook](../facebook/SKILL.md) tools. Follow `next_cursor` within the requested scope. The cursor keeps the first page's `limit` and `unread` filter. Pages from several accounts can hold fewer items than `limit` to keep the order. Report `skipped` accounts (signed out or restricted) and `errors` with their next step, and do not claim the whole inbox was checked when accounts were skipped or more pages remain.

Use `inbox_get_messages` with the chat's `chat_id` and `account_id`. Messages arrive most recent first. Check who sent the latest message and read the exchange in chronological order. An unread count or snippet alone does not prove the user owes a reply. Attachment metadata does not reveal attachment contents.

Present the network, the person or group name, the latest inbound request, its timestamp, and a suggested next action. Group the summary by network when several are involved. State the number of conversations inspected.

## Draft and send replies

Draft replies from the conversation's facts and the user's requested tone, in the register of that network: chat apps are usually shorter and less formal than LinkedIn. Keep commitments, dates, and claims grounded in the conversation or the user's instructions.

Show the network, the recipient or group, and the exact text before calling `inbox_send_message` with `chat_id`, `account`, and `text`. Send only after the user authorizes that reply. If they already approved that exact draft, proceed without another approval request. In a group chat, the reply goes to every member: say so when it matters. To send an image with the message (one per message), add `image_url`, a public `https` link to a JPEG, PNG, or WebP image of at most 8 MB, or `media_id` from `upload_image` for an image on the user's device or attached in the chat: give the user the upload link and wait until they say it's uploaded. If you made the image yourself and can run commands with internet access (a code sandbox, a terminal), upload it yourself with the `upload_command` that `upload_image` returns, and pass the `media_id` once it answers `ok`. Show the image with the text before sending.

Confirm success from the tool result. If the outcome is uncertain, inspect the conversation with a fresh read before retrying.

## Start a conversation

Use `inbox_start_chat` with `to`, `text`, and `account` only when the user asks to message someone they have no conversation with. `to` is a LinkedIn `person_id`, a WhatsApp phone number in international format with its country code, or a Telegram, Instagram, or Facebook user id (a chat's `person_id`). Starting chats has a low daily limit. WhatsApp, Telegram, Instagram, and Facebook restrict accounts that message strangers, so only message people who expect it, and show the recipient and exact text first. For LinkedIn InMail, invitations, or batches, use [LinkedIn outreach](../linkedin-outreach/SKILL.md).

## Read state

Reading or summarizing does not authorize `inbox_mark_read`. Use it when the user asks to mark a conversation read or unread, with the chat's `account`.

## Network-specific tools

The `linkedin_*`, `whatsapp_*`, `telegram_*`, `instagram_*`, and `facebook_*` tools do the same on one network, and their `list_chats` merges that network's accounts. Prefer them when the user names a single network. For reactions, profiles, group members, or Instagram posts, use [WhatsApp, Telegram and Instagram](../whatsapp-telegram-instagram/SKILL.md). For Facebook Pages, message requests, posts, comments, reactions, profiles, or friends, use [Facebook](../facebook/SKILL.md). For LinkedIn-only triage, use [LinkedIn inbox](../linkedin-inbox/SKILL.md).
