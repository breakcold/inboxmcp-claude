# InboxMCP for LinkedIn

Manage your LinkedIn, WhatsApp, Telegram and Instagram inboxes from Claude. InboxMCP finds conversations waiting for a reply across every connected account, drafts responses grounded in the thread, researches LinkedIn profiles, and prepares outreach that only goes out after you approve the recipients and the exact text.

## What's included

- **MCP server**: connects Claude to the hosted InboxMCP server at `https://inbox-mcp.com/mcp` over streamable HTTP. You sign in through OAuth in your browser. The plugin contains no credentials.
- **`inbox` skill**: one inbox across LinkedIn, WhatsApp, Telegram and Instagram. It lists conversations from every connected account, reads threads, drafts replies, and sends or starts a conversation only after you approve it.
- **`whatsapp-telegram-instagram` skill**: chats on those networks plus reactions, contact profiles, group members, and approved Instagram photo posts.
- **`linkedin-inbox` skill**: triage unread messages and conversations you owe a reply to, read threads, and draft replies. It sends a reply only after you approve it.
- **`linkedin-research` skill**: search people, look up a profile, and draft an introduction from verified profile facts. Research never sends anything.
- **`linkedin-outreach` skill**: send approved messages and connection requests, schedule a paced batch, check per-item delivery results, and publish approved text posts.

## Requirements

- An InboxMCP account with at least one connected LinkedIn, WhatsApp, Telegram or Instagram account. New workspaces start with a free trial, then need a paid subscription. Billing happens on [inbox-mcp.com](https://inbox-mcp.com) through Stripe, not in chat.
- Claude Code, Claude Desktop, or claude.ai with plugin or connector support.

## Install

In Claude Code:

```bash
claude plugin marketplace add breakcold/inboxmcp-claude
```

```bash
claude plugin install inboxmcp@inboxmcp
```

Then run `/mcp`, select `inboxmcp`, and finish the OAuth sign-in in your browser. Ask "Check my LinkedIn account connection" to verify the setup.

## Example prompts

- "Show my unread messages across LinkedIn, WhatsApp, Telegram and Instagram and draft replies. Don't send them."
- "Find LinkedIn conversations waiting for my reply and draft a response. Don't send it."
- "Research https://www.linkedin.com/in/someone and draft a short introduction."
- "Prepare connection requests for these five people and show me the notes before sending."

## Safety

- Reading, summarizing, and drafting never send anything. Sends, invitations, posts, and scheduled batches run only after you approve the exact text and recipients.
- InboxMCP paces every action and enforces each network's daily and weekly limits. The plugin respects cooldowns and never retries a write automatically.
- Scheduled outreach can't be canceled, paused, or resumed through the plugin. Posts can't be edited or deleted.

## Data and privacy

This plugin runs no local code. It only declares the remote MCP server above. Tool calls send your requests to InboxMCP, which reads and writes LinkedIn, WhatsApp, Telegram and Instagram data through its provider Unipile and returns the results to Claude. InboxMCP doesn't store message or profile content in its database. Approved scheduled message text is held until delivery. See the [privacy policy](https://inbox-mcp.com/privacy) and [terms of service](https://inbox-mcp.com/terms) for retention, deletion, and contact details.

## Support

Documentation and the support contact are at [inbox-mcp.com/docs](https://inbox-mcp.com/docs).

## License

MIT. See [LICENSE](LICENSE).
