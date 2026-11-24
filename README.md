# Dial by Behaf

**An MCP server that lets Claude make outbound phone calls to Indian businesses. Works with Claude and Claude Code.**
You ask in plain words. Dial calls the clinic, the shop or the service centre, talks to the person who answers, and brings back what they said.

```bash
claude mcp add --transport http dial https://dial.behaf.co/mcp
```

[Docs](https://www.behaf.co/dial-docs) · [Setup page](https://www.behaf.co/mcp) · [Discussions](https://github.com/behaf/dial-mcp/discussions) · [MCP Registry: `co.behaf/dial`](https://registry.modelcontextprotocol.io/v0/servers?search=co.behaf)

<a href="https://www.behaf.co/dial?src=github"><img src="assets/dial-you-ask-dial-calls.jpg" alt="Dial by Behaf. You ask. Dial calls." width="640"></a>

---

## What a call looks like (example)

```text
you     > Call Sunrise Clinic on +91 XXXXXXXXXX. Ask if there is a knee check-up slot on Saturday morning. Don't book.
claude  > prepare_call  → playbook: enquiry · they may ask: patient name, age, first visit?
claude  > Here is the plan. Shall I call?
you     > yes
claude  > place_call    → call_id c_…
claude  > get_call      → ringing → talking → ended
claude  > Partly done. They have a slot at 11:30, but the doctor confirms at 9 am on Saturday.
```

Every call ends with a status (`done`, `partly`, `failed`, `no_answer`), a typed outcome, a summary and the full transcript.


## Connect

| App | How |
|---|---|
| Claude (web, desktop) | Settings → Connectors → Add custom connector → name `Dial`, URL `https://dial.behaf.co/mcp` → sign in |
| Claude Code | `claude mcp add --transport http dial https://dial.behaf.co/mcp` |

Dial works with Claude (web, desktop, mobile) and Claude Code. Streamable HTTP, OAuth sign-in, no API keys. `https://dial.behaf.co/mcp` is a connector address, not a web page.

## Access

Dial is in early access. We open it to a few people at a time, so every call can be done well.

**Developers:** join the developer list at https://www.behaf.co/dial?dev=1&src=github#join. We'll email you when your access opens, with the steps to sign in at https://dial.behaf.co and set up your wallet. Then add the URL above.

## Try it

Ask for a call in plain words. Your assistant runs `prepare_call` first: it places no call and costs nothing, and shows you the plan and the questions the business will probably ask. It calls only when you say yes.

Start with something small: a shop's opening hours, a stock check, a price. Then read the transcript and check the summary against it.

## Tools

| Tool | What it does | Type |
|---|---|---|
| `prepare_call` | Readiness check, no call placed: picks the playbook, lists missing info and the questions the business is likely to ask | read-only |
| `place_call` | Places the call. Returns a call ID; the call runs in the background | action |
| `get_call` | Waits for a change, then returns status, phase (menu, hold, talking), latest lines, and the result when the call ends | read-only |
| `get_call_transcript` | Full turn-by-turn transcript | read-only |
| `answer_call_question` | Sends your answer when the business asks something Dial isn't allowed to decide | action |
| `list_calls` | Your recent calls | read-only |
| `cancel_call` | Cancels a queued call or ends a live one | action |
| `get_account` | Wallet balance and terms status | read-only |

## Design choices

- **Ask before dialling.** `prepare_call` lists what the business will probably ask, so you answer before the call, not halfway through it.
- **Ask, don't guess.** If the business asks something you didn't allow (a time, a price), the call relays the question to you with `answer_call_question`.
- **Call content is untrusted.** What the other side says comes back fenced as data, never as instructions to your assistant. A voice on the line can't steer your agent.
- **Honest results.** Calls fail. Lines are busy, people hang up. Dial reports that plainly instead of pretending.

## Languages

Calls can open in English, Hindi, Bengali, Tamil, Telugu, Kannada, Malayalam, Marathi, Gujarati, Punjabi and Odia, and follow the other side if they switch. We have checked English, Hindi, Tamil and Malayalam by ear; the others are switched on and less tested. Tell us how they sound.

## Rules on every call

- Dia, the voice, says she is an AI assistant calling on your behalf.
- Your assistant confirms the number and the plan with you before calling.
- Outbound only. One person's errand to one business at a time. No telemarketing, bulk calls, impersonation, threats or debt collection.
- Dial never asks anyone for OTPs, passwords, card or bank details, or Aadhaar numbers.
- Anyone can say "don't call me again".
- Indian (+91) numbers only for now.

## Price

See https://www.behaf.co/dial-pricing. Calls are paid from a prepaid Dial wallet.

## Data

No call audio is recorded. Dial keeps your call requests, transcripts and summaries so you can check what was said; you can delete them at any time. [Privacy](https://www.behaf.co/dial-privacy) · [Terms](https://www.behaf.co/dial-terms)

## Build Dial with us

Imagine you had a personal assistant who handles your calls. Now imagine you could build on it.

Dial is early, and developers shape what it becomes:
- **Ideas:** what should Dial do next? Post in [Discussions → Ideas](https://github.com/behaf/dial-mcp/discussions/categories/ideas).
- **Bugs and odd calls:** open a [discussion in Q&A](https://github.com/behaf/dial-mcp/discussions/categories/q-a) with what you asked and what happened (no personal phone numbers, please).
- **Show what you built:** [Show and tell](https://github.com/behaf/dial-mcp/discussions/categories/show-and-tell).

Every change that comes from your idea goes into the [CHANGELOG](CHANGELOG.md) with your name. Start here: [Build Dial with us](https://github.com/behaf/dial-mcp/discussions/1).

## Support

Questions and bugs: [Discussions](https://github.com/behaf/dial-mcp/discussions). Email: jerish@behaf.co

---

Dial by Behaf is not affiliated with or endorsed by Anthropic. Claude is a trademark of Anthropic.
