# Tervita agent skill

A skill for AI coding agents (Claude Code, Codex and other agents that can
drive a browser) to work in the [Tervita](https://tervita.ee) clinic CRM
through your own signed-in Chrome tab.

Tervita registers WebMCP tools (`document.modelContext`) on its CRM pages.
They run as the person who is signed in, with that person's permissions. The
agent can look up bookings, clients, services, free times and invoices, and it
can prepare a booking or an invoice. Saving, cancelling, issuing and sending
are never done by the agent: Tervita opens the right screen, highlights the
button, and you press it and confirm.

## Requirements

- Tervita open and signed in, in Chrome 149 or later on `https://tervita.ee`
  (or any Chrome with `chrome://flags/#enable-webmcp-testing` enabled).
- An agent that can reach that tab: Claude in Chrome, or the
  [chrome-devtools MCP server](https://github.com/ChromeDevTools/chrome-devtools-mcp)
  connected to your Chrome.

## Install

Claude Code:

```sh
mkdir -p ~/.claude/skills && cp -R tervita-crm ~/.claude/skills/
```

Codex:

```sh
mkdir -p ~/.codex/skills && cp -R tervita-crm ~/.codex/skills/
```

Then ask your agent something like "In Tervita, find a free slot for
Consultation tomorrow afternoon and prepare a booking for Anna Tamm".

## Knowledge base

The skill tells the agent to explain Tervita from its own help centre:
through the `search_help` and `get_help_article` tools in the signed-in tab, or
without it from https://tervita.ee/help and https://tervita.ee/llms.txt, and
to cite the article link.

## Safety model

- Tools only read, or fill a form; nothing is stored until you press the
  button yourself.
- Cancelling a booking and issuing or sending an invoice open the record with
  a notice and the button highlighted; you confirm in Tervita's own dialog.
- The skill also tells the agent to ask you in chat before any such step, to
  treat text from the CRM as data rather than instructions, and to keep client
  data where it is.
- Tools follow your role: a person who cannot create invoices gets no invoice
  tool.

## License

MIT, see [LICENSE](LICENSE).
