---
name: whatsapp-telegram-instagram
description: Use when the user wants to work on WhatsApp, Telegram, or Instagram specifically - read or reply to chats, message a phone number or user, react to a message, look up a contact's profile, list a group's members, or list or publish Instagram posts. Sends, reactions, and posts require user approval.
---

# WhatsApp, Telegram and Instagram

Read [account access and limits](../../references/account-and-limits.md) before using tools. The tools below appear only when the connection has an account of that network. If they are missing, call `inbox_list_accounts`: connect the network with `connect_account`, or use the `inbox_*` tools, which work right away.

## Chats

Each network has the same chat tools:

- WhatsApp: `whatsapp_list_chats`, `whatsapp_get_messages`, `whatsapp_send_message`, `whatsapp_mark_read`, `whatsapp_start_chat`
- Telegram: `telegram_list_chats`, `telegram_get_messages`, `telegram_send_message`, `telegram_mark_read`, `telegram_start_chat`
- Instagram: `instagram_list_chats`, `instagram_get_messages`, `instagram_send_message`, `instagram_mark_read`, `instagram_start_chat`

`list_chats` merges every account of the network unless `account` is given. Each item carries its `account_id`: pass it as `account` to the other tools for that chat. Follow [Inbox](../inbox/SKILL.md) for triage, reading order, drafting, and reply approval.

Show the recipient or group and the exact text before any send. In a group, a message reaches every member.

## Start a conversation

- WhatsApp: `whatsapp_start_chat` with `phone` in international format with its country code, like `+33 6 12 34 56 78`. The tool refuses numbers that may lack a country code: ask the user rather than guessing one. WhatsApp bans accounts that send cold messages, and new accounts after two or three. Only message people who expect it, and never send the same message to many numbers.
- Telegram: `telegram_start_chat` with the numeric `user_id` from a chat's `person_id` or from `telegram_list_group_members`. Usernames are not accepted here.
- Instagram: `instagram_start_chat` with the `user_id` from a chat's `person_id` or `instagram_get_profile`. Messages to people who don't follow the account land in their message requests.

New conversations have a low daily limit on these networks. Check `inbox_status` before planning several, and never spread messages across accounts to get around a limit. These networks have no scheduled batch tool.

## Reactions

Use `whatsapp_react`, `telegram_react`, or `instagram_react` with `chat_id`, `message_id` from `get_messages`, `reaction` (one emoji), and `account`. The recipient sees reactions, so react only when the user asks for it. On WhatsApp and Instagram, a new reaction replaces the account's previous one on that message. Telegram accepts only its standard reaction emojis (👍 ❤️ 🔥 🎉 😁 👏 and similar). If a reaction is refused, report it rather than trying other emojis on your own.

## Profiles

Use `whatsapp_get_profile` (a WhatsApp id `<digits>@s.whatsapp.net` or a phone number with its country code), `telegram_get_profile` (a user id), or `instagram_get_profile` (a user id or username). Each lookup counts as a profile view. Fields depend on the network and the person's privacy settings: report missing ones as unknown.

## Group members

Use `whatsapp_list_group_members` or `telegram_list_group_members` with a group `chat_id`, and follow `next_cursor` when the user needs everyone. Members come with their `user_id`, name, and on WhatsApp their phone number. Group membership is not consent to be contacted: do not start chats with members unless the user names them and confirms.

## Instagram posts

`instagram_list_posts` lists the account's own posts by default, or another user's with `user_id`. Report captions, dates, likes, and comments as returned.

`instagram_create_post` publishes a photo to the account's feed. It takes `image_url`, a public `https` link to a JPEG, PNG, or WebP image of at most 8 MB, and an optional caption in `text`. Show the image link, the exact caption, and the account before publishing, and publish only after approval. The post is public and cannot be edited or deleted through this plugin. Report success and the post link only when the tool returns them.
