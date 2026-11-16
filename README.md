# Dial by Behaf

Let your AI assistant make real phone calls to Indian businesses.

Dial is a remote [MCP](https://modelcontextprotocol.io) server. Add it to Claude, Claude Code, Cursor or another MCP client, ask for a call in plain words, and your assistant phones the business, gets through the menu and the hold music, talks to the person who answers, and brings back a summary, the outcome and the transcript.

- Website: https://www.behaf.co/dial
- Docs: https://www.behaf.co/dial-docs
- Sign in and wallet: https://dial.behaf.co
- MCP Registry: `co.behaf/dial`

## Connector URL

```
https://dial.behaf.co/mcp
```

Streamable HTTP, OAuth sign-in. **This is a connector address, not a web page**: add it inside your AI app. Opening it in a browser shows an error.

## Connect

**Claude (web, desktop):** Settings → Connectors → Add custom connector → name `Dial`, URL `https://dial.behaf.co/mcp` → sign in.

**Claude Code:**

```bash
claude mcp add --transport http dial https://dial.behaf.co/mcp
```

**Cursor and other MCP clients** (`mcp.json`):

```json
{
  "mcpServers": {
    "dial": { "url": "https://dial.behaf.co/mcp" }
  }
}
```

**ChatGPT (Business, Enterprise, Edu):** a workspace admin adds a custom MCP server with the same URL and OAuth.

## Try it

> Call Sunrise Clinic on +91 XXXXXXXXXX and ask if they have a slot for a knee check-up on Saturday morning. Don't book, just ask.

Your assistant runs a free check first, asks you what the business will probably ask (a name, a time, a budget), shows you the plan, and calls only when you say yes.

## Tools

| Tool | What it does |
|---|---|
| `prepare_call` | Free readiness check, no call placed: picks the playbook (booking, enquiry, customer care, follow-up, cancellation), lists missing info and likely questions, drafts the brief. |
| `place_call` | Places the call. Returns a call ID; the call runs in the background. |
| `get_call` | Waits for a change, then returns status, phase (menu, hold, talking), latest lines, and the summary and outcome when the call ends. |
| `get_call_transcript` | Full turn-by-turn transcript. |
| `answer_call_question` | Sends your answer when the business asks something Dial isn't allowed to decide. |
| `list_calls` | Your recent calls. |
| `cancel_call` | Cancels a queued call or ends a live one. |
| `get_account` | Wallet balance, rates and terms status. |

Languages a call can open in: English (`en-IN`), Hindi, Bengali, Tamil, Telugu, Kannada, Malayalam, Marathi, Gujarati, Punjabi and Odia. Dial follows the other side if they switch.

## Rules on every call

- The call opens by saying an AI is calling on your behalf.
- Your assistant confirms the number and the plan with you before calling.
- Person-to-business errands, one at a time. No telemarketing, bulk calling, impersonation, threats or debt collection.
- Dial never asks anyone for OTPs, passwords, card or bank details, or Aadhaar numbers.
- Anyone can say "don't call me again".
- What the other party says comes back fenced as untrusted content, never as instructions to your assistant.

## Price

₹5 a minute plus GST, billed by the second. Prepaid wallet at https://dial.behaf.co (UPI or card).

## Data

No call audio is recorded. Dial keeps your call requests, written transcripts and summaries so you can check what was said; you can delete your data at any time. See the [privacy page](https://www.behaf.co/dial-privacy) and [terms](https://www.behaf.co/dial-terms).

## Support

jerish@behaf.co
