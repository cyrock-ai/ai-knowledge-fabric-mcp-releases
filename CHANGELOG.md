# Changelog

Each release works with the AI Knowledge Fabric versions of the same major (`1.x` with `1.x`).

## 1.4.0 - 2026-11-27

- Pipeline names may now contain digits and hyphens (`-`), for example `Report-2026`. A name must still start
  with a letter or `_`.
- For administrators: the address of an Anthropic (Cloud), OpenAI (Cloud) or Google Gemini (Cloud) server is
  fixed. For any other address, for example a gateway or another cloud vendor, Claude registers the server as
  OpenAI API (self-hosted).

## 1.3.0 - 2026-11-20

- For administrators: tool providers, which are other systems' MCP servers (a ticket system, a CRM) where each
  user signs in with their own account. You can list, find the sign-in details of, register, change and remove
  them. Their client secrets are entered on the admin page, never in the chat. Needs an instance with tool
  providers.
- Pipelines: agents can use another system's MCP server as each user (Remote MCP Server module with user
  sign-in). Before a pipeline uses one shared account for everyone, Claude asks whether that is intended. The
  shared token is entered in the Pipeline Designer.
- GraphRAG topics: set how many earlier messages a topic remembers and what it answers when it finds nothing.

## 1.2.0 - 2026-11-02

- Pipelines: list, show, build, change module by module, and delete; the Pipeline Designer opens them as usual.
- Content rules (guardrails) of RAG and GraphRAG topics: set and change them with the topic.
- Evaluation: test sets and their questions, runs against a topic, results, findings, what happened for one
  question, comparison of two runs, and analysis with suggested changes. Needs an instance with the evaluation API.
- For administrators: register, change, check and remove AI servers, Docling servers, vector and graph
  databases, and start or stop the servers the instance runs itself. Needs an instance with these API routes.
- An overview at the start of a session, with what needs attention and suggested next steps.
- Claude now lists the settings it chose and asks before every change (create, change, start, stop, delete).

Fixes:

- Restarting a topic that was in error no longer reports "failed to start" by mistake.
- Several tool calls finishing at the same time no longer lose answers.
- Removing a setting from a pipeline module (sending it as empty) now works.

## 1.0.0 - 2026-10-14

First release.

- Manage RAG topics, GraphRAG topics and agents: list, show, create, change, start, stop and delete; assign
  pipelines to agents.
- Connect through a page in the browser: no settings in the AI assistant, the token never goes through the chat.
- Claude Desktop extension, Claude Code plugin, and programs for other MCP clients, for Windows and Linux. macOS
  follows in a later release.
