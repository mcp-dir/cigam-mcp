# Instalação rápida

CIGAM é um servidor MCP remoto hospedado em `https://api.mcp.ai/p_cigam`. Você não baixa nem roda nada localmente — só aponta seu cliente pra essa URL.

A auth acontece em runtime: clientes com **OAuth 2.1** (Claude Desktop, Cursor, VS Code recentes) abrem o browser na 1ª chamada (magic-link). Clientes sem OAuth recebem a tool `authenticate` — abra `https://app.mcp.ai/agent-auth`, faça login, copie o JWT e cole no chat.

---

## Claude (Web e Desktop)

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → `CIGAM` / `https://api.mcp.ai/p_cigam`.

Config file (legado): `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) ou `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{ "mcpServers": { "cigam": { "type": "http", "url": "https://api.mcp.ai/p_cigam" } } }
```

## Cursor

[➕ Instalar no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=cigam&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9jaWdhbSJ9)

`.cursor/mcp.json`:
```json
{ "mcpServers": { "cigam": { "url": "https://api.mcp.ai/p_cigam" } } }
```

## VS Code (Copilot Chat)

[➕ Instalar no VS Code](vscode:mcp/install?name=cigam&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_cigam%22%7D)

`.vscode/mcp.json`:
```json
{ "servers": { "cigam": { "type": "http", "url": "https://api.mcp.ai/p_cigam" } } }
```

## Outros clientes MCP

Qualquer cliente com **MCP over HTTP**. URL fixa:

```
https://api.mcp.ai/p_cigam
```

Dúvidas? [cigam@mcp.ai](mailto:cigam@mcp.ai)
