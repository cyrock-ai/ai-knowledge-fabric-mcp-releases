# AI Knowledge Fabric for Claude and other AI assistants

Create and manage your AI Knowledge Fabric topics, GraphRAG topics, agents and pipelines by talking to your AI
assistant. It can also test how well a topic answers, and, for administrators, register the AI servers, Docling
servers and databases the topics run on. This repository holds the downloads and the Claude plugin; you need
nothing else.

The assistant works with your own account and permissions, through your instance's Management REST API. It runs
on your computer, so it reaches your instance wherever your browser does, including over VPN. It asks you before
every change.

## Before you start

1. Your AI Knowledge Fabric account needs the **`API_ACCESS`** permission, plus the usual permissions for what
   you want to do (for example creating topics). The default `USER` role does not include `API_ACCESS`; ask an
   administrator to grant it. Two areas need permissions of their own:
   - **Testing topics (evaluation):** `EVALUATION_VIEW` to see test sets and runs, `EVALUATION_RUN` to change
     them, and `DEV_REPORTING` to start runs and see what happened for a question.
   - **Registering servers and databases:** `SERVER_MANAGE`, the permission of the admin pages.
2. Create a **personal access token** on your Profile page in AI Knowledge Fabric. It starts with `kfp_` and is
   shown only once; keep it at hand for step 2 below.

## 1. Install

Pick what fits where you use Claude. Using Claude Desktop's Chat tab *and* Claude Code? Do both; they share one
connection.

### Claude Desktop (Chat tab)

1. Download the extension for your computer:
   - [Windows](https://github.com/cyrock-ai/ai-knowledge-fabric-mcp-releases/releases/latest/download/ai-knowledge-fabric-mcp-win32-x64.mcpb)
   - macOS: coming in a later release
   - [Linux](https://github.com/cyrock-ai/ai-knowledge-fabric-mcp-releases/releases/latest/download/ai-knowledge-fabric-mcp-linux-x64.mcpb)
2. In Claude Desktop, open **Settings → Extensions**, drag the file onto the page and choose **Install**. Leave
   the instance address and token empty.
3. Quit Claude completely and open it again. Closing the window is not enough:
   - **Windows:** right-click the Claude icon in the notification area at the right end of the taskbar (behind
     the **^** arrow if hidden) and choose **Exit**.
   - **macOS:** press **⌘Q** in Claude.

### Claude Code (Claude Desktop's Code tab, terminal, IDEs)

Run in a terminal:

```bash
claude plugin marketplace add cyrock-ai/ai-knowledge-fabric-mcp-releases
```

```bash
claude plugin install ai-knowledge-fabric@cyrock-ai
```

Then quit Claude completely and open it again (see above). The plugin is then there in the terminal, in your
IDE and in Claude Desktop's Code tab. These commands need Claude Code's command line (`claude`); if your
terminal does not know it, [install it](https://code.claude.com/docs/en/setup) first.

> **Not through Claude Desktop's "Add marketplace" button.** It currently refuses this plugin with "Marketplace
> sync failed": it does not accept a plugin that brings its program as a download. Use the commands above.

New versions:

```bash
claude plugin marketplace update cyrock-ai
```

```bash
claude plugin update ai-knowledge-fabric@cyrock-ai
```

If your organisation's administrator already made the plugin available or installed it for everyone, it is
there without these steps.

### VS Code, Cursor and other MCP clients

Download the program for your computer and put it in a folder where it can stay, for example `C:\Tools\` or
`~/bin/`:

- [Windows](https://github.com/cyrock-ai/ai-knowledge-fabric-mcp-releases/releases/latest/download/ai-knowledge-fabric-mcp-win32-x64.exe)
- macOS: coming in a later release
- [Linux](https://github.com/cyrock-ai/ai-knowledge-fabric-mcp-releases/releases/latest/download/ai-knowledge-fabric-mcp-linux-x64)

On macOS and Linux, make it executable: `chmod +x ~/bin/ai-knowledge-fabric-mcp-*`.

Then register it as a local (stdio) MCP server, with no further settings.

VS Code: run **MCP: Open User Configuration** and add

```json
{
  "servers": {
    "ai-knowledge-fabric": { "type": "stdio", "command": "C:\\Tools\\ai-knowledge-fabric-mcp-win32-x64.exe" }
  }
}
```

Cursor: add the same to `~/.cursor/mcp.json`, with `mcpServers` in place of `servers`.

## 2. Connect (once per computer)

Ask your assistant: *"Connect to AI Knowledge Fabric."*

A page opens in your browser. Enter your instance's address, as you open AI Knowledge Fabric in the browser,
and paste your token there. **Never paste the token into the chat.** The page checks the connection and shows
what your account may see.

The connection is then saved on this computer and used by every Claude product and MCP client on it. On
Windows the token is encrypted for your user account; on macOS and Linux it is kept in a file only you can read.

## 3. Use it

Ask for what you need, for example *"Create a GraphRAG topic for our product manuals."* The assistant looks up
the AI servers, models and databases your instance offers, asks you what it needs to know, and shows you every
change before making it.

More examples:

- *"Build an agent that answers support questions from our manuals topic."* The assistant builds the pipeline,
  creates the agent and assigns the pipeline to it.
- *"Block questions about competitors in the sales topic."* The assistant sets up the topic's content rules
  (guardrails).
- *"Make a test set from these ten questions and run it against the manuals topic."* Then *"Why are the answers
  weak?"* or *"Did raising the minimum score help?"*: the assistant reads the findings, explains a weak answer,
  and compares two runs. It only suggests changes; it makes one only after you agree.
- *"Register our Qdrant server at qdrant.internal."* (administrators): the assistant registers it and checks
  that it answers. Enter passwords and API keys on the admin pages rather than in the chat.
- *"Check the connection to AI Knowledge Fabric"* shows the instance, the version of this server and what your
  account may see.
- To switch to another instance or replace an expired token, ask to connect again.

## Troubleshooting

| What happens | What to do |
| --- | --- |
| Claude says it has no AI Knowledge Fabric tools | Check that the extension or plugin is installed and switched on, then quit Claude completely and reopen it. In Claude Desktop's Code tab, use the plugin: the extension reaches Code sessions only some of the time. |
| "Marketplace sync failed" in Claude Desktop | The **Add marketplace** button does not accept this plugin yet. Use the terminal commands under "Claude Code". |
| The plugin has fewer tools than described here | An older copy of the marketplace is in use. Run the two commands under "New versions", then restart Claude. |
| The connect page does not open | Claude shows the link in the chat; open it in your browser. The page only works on the computer the assistant runs on: over SSH, in WSL or in a container, see "Configuration" below. |
| The page warns about an unencrypted address | Your address starts with `http://`. Use the `https://` address if your instance has one. |
| "The bearer token is unknown, revoked or expired" | Create a new token on your Profile page and connect again. |
| "…does not have the API_ACCESS permission" | Ask an administrator to grant it. |
| A certificate error | Your organisation uses its own certificate authority. Open **Company certificate** on the connect page and enter the path of its PEM file. |
| macOS refuses to open the program | Allow it under **System Settings → Privacy & Security**, or run `xattr -d com.apple.quarantine <path to the program>`. |

To remove the saved connection, delete `connection.json` in the folder `.ai-knowledge-fabric-mcp` in your home
folder.

## Configuration

Usually not needed: the connect page covers it. For clients where the page cannot be used, the server also
reads these environment variables. When they include a token, they win over a saved connection.

| Variable | Example | Meaning |
| --- | --- | --- |
| `KF_URL` | `https://kf.example.com` | Address of your instance |
| `KF_API_TOKEN` | `kfp_…` | Your personal access token |
| `KF_CA_FILE` | `C:\certs\company-ca.pem` | Optional: your organisation's certificate authority |

## Versions

Releases follow the major version of AI Knowledge Fabric: `1.x` works with AI Knowledge Fabric `1.x`. A tool
that needs a newer instance than yours says so. See
[CHANGELOG.md](CHANGELOG.md) for what changed, and [SECURITY.md](SECURITY.md) to report a security problem.
