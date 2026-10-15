# Scalable Claude Code plugin

Use Scalable's hosted MCP tools to create and improve Amazon listing images and A+ content. The plugin connects to Scalable at https://scalable.so/api/mcp; sign in when Claude Code prompts you to authorize access.

## Install in Claude Code

In Claude Code, add the public plugin repository as a marketplace and install the plugin:

```text
/plugin marketplace add scalable-so/scalable-claude-plugin
/plugin install scalable@scalable
```

## Install in claude.ai

Download `scalable-claude-ai.zip` from this repository, then upload it in claude.ai under **Customize → Skills → Add skill → Upload a skill**. The skill needs Scalable's tools: add a custom connector with the URL https://scalable.so/api/mcp and sign in when claude.ai asks.

The `scalable` skill guides product workflows and follows server-generated MCP session rules.
