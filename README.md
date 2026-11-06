# Pluggzy

Manage your LinkedIn, WhatsApp, Telegram and Instagram messages from Claude. Pluggzy finds conversations waiting for a reply across every connected account, drafts responses grounded in the thread, researches LinkedIn profiles, publishes or schedules LinkedIn and Instagram posts, and prepares outreach. Nothing is sent, posted, or scheduled until you approve the recipients, the exact text, and any image.

## What's included

- **MCP server**: connects Claude to the hosted Pluggzy server at `https://pluggzy.com/mcp` over streamable HTTP. You sign in through OAuth in your browser. The plugin contains no credentials.
- **`inbox` skill**: one inbox across LinkedIn, WhatsApp, Telegram and Instagram. It lists conversations from every connected account, reads threads, drafts replies, and sends or starts a conversation only after you approve it.
- **`whatsapp-telegram-instagram` skill**: chats on those networks plus reactions, contact profiles, group members, and approved Instagram photo posts, published now or scheduled.
- **`linkedin-inbox` skill**: triage unread messages and conversations you owe a reply to, read threads, and draft replies. It sends a reply only after you approve it.
- **`linkedin-research` skill**: search people, look up a profile, and draft an introduction from verified profile facts. Research never sends anything.
- **`linkedin-outreach` skill**: send approved messages and connection requests, schedule a paced batch, check per-item delivery results, and publish or schedule approved LinkedIn posts, with an optional image. List upcoming scheduled posts and cancel one before it goes out.

## Requirements

- A Pluggzy account with at least one connected LinkedIn, WhatsApp, Telegram or Instagram account. New workspaces start with a free trial, then need a paid subscription. Billing happens on [pluggzy.com](https://pluggzy.com) through Stripe, not in chat.
- Claude Code, Claude Desktop, or claude.ai with plugin or connector support.

## Install

In Claude Code:

```bash
claude plugin marketplace add breakcold/inboxmcp-claude
```

```bash
claude plugin install pluggzy@pluggzy
```

Then run `/mcp`, select `pluggzy`, and finish the OAuth sign-in in your browser. Ask "Check my LinkedIn account connection" to verify the setup.

## Example prompts

- "Show my unread messages across LinkedIn, WhatsApp, Telegram and Instagram and draft replies. Don't send them."
- "Find LinkedIn conversations waiting for my reply and draft a response. Don't send it."
- "Research https://www.linkedin.com/in/someone and draft a short introduction."
- "Prepare connection requests for these five people and show me the notes before sending."
- "Draft a LinkedIn post about our launch and schedule it for Tuesday at 9am once I approve it."

## Safety

- Reading, summarizing, and drafting never send anything. Sends, invitations, reactions, posts, and scheduled batches run only after you approve the exact text, recipients, and image.
- Pluggzy paces every action and enforces each network's daily and weekly limits. The plugin respects cooldowns and never retries a write automatically.
- Scheduled posts can be listed and canceled before they publish. Scheduled outreach batches can't be canceled, paused, or resumed through the plugin. Published posts can't be edited or deleted.

## Data and privacy

This plugin runs no local code. It only declares the remote MCP server above. Tool calls send your requests to Pluggzy, which reads and writes LinkedIn, WhatsApp, Telegram and Instagram data through its provider Unipile and returns the results to Claude. Pluggzy doesn't store message or profile content in its database. Approved scheduled message and post content, and images you upload for a post or message, are held until delivery. See the [privacy policy](https://pluggzy.com/privacy) and [terms of service](https://pluggzy.com/terms) for retention, deletion, and contact details.

## Support

Documentation and the support contact are at [pluggzy.com/docs](https://pluggzy.com/docs).

## License

MIT. See [LICENSE](LICENSE).
