# CIGAM

### CIGAM for Claude, ChatGPT and AI agents

CIGAM ERP (management for industry, retail and franchises) via session capture with your authorization. Since CIGAM has no public API, you provide your access key, user and password and the platform logs into your account to read your own data, on the same API the CIGAM portal uses. Read-only: sales, invoices, accounts payable and receivable, cash register closings, financial entries and suppliers.

- 📊 **22 tools**
- ✏️ **Read and write**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → name `CIGAM`, URL `https://api.mcp.ai/p_cigam`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=cigam&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9jaWdhbSJ9)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=cigam&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_cigam%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_cigam
```

---

## 22 tools

| Tool | Description |
|---|---|
| `cigam_list_accounts` | Lista as contas CIGAM conectadas a este install — id, label (instância/usuário). |
| `cigam_listar_lojas` | Lista as lojas/empresas que a conta enxerga (código, nome, CNPJ). |
| `cigam_notas_fiscais` | Lista notas fiscais de uma loja por período. |
| `cigam_vendas` | Vendas de uma loja por período (notas fiscais de saída do tipo Venda). |
| `cigam_compras` | Compras de uma loja por período (notas fiscais de entrada do tipo Compra). |
| `cigam_devolucoes` | Devoluções de uma loja por período (notas fiscais com movimento de devolução, entrada e saída). |
| `cigam_vendas_resumo` | Panorama do período numa loja: totais de vendas, compras e devoluções (quantidade e valor de cada). |
| `cigam_fluxo_caixa` | Fluxo de caixa projetado de uma loja por período: total a receber (contas a receber em aberto) vs total a pagar (contas a pagar), e o saldo projetado. |
| `cigam_ranking_clientes` | Ranking de clientes por valor vendido no período (agrupa as vendas por destinatário/CNPJ-CPF). |
| `cigam_vendas_por_dia` | Série de vendas por dia no período (quantidade e valor por data) + resumo com total e ticket médio. |
| `cigam_inadimplencia` | Contas a receber vencidas e ainda em aberto (inadimplência). |
| `cigam_resultado` | Resultado gerencial simplificado de uma loja por período: receita (vendas faturadas líquidas de devolução) menos despesas (lançamentos financeiros por plano de contas), com o detalhe das despesas por categoria. |
| `cigam_formas_pagamento` | Mix de formas de recebimento de uma loja por período: total recebido por forma de pagamento, por bandeira de cartão e por adquirente (maquininha). |
| `cigam_relatorio` | Gera um relatório do CIGAM (operação LENTA, ~2 min, produz um arquivo Excel). |
| `cigam_job` | Busca o resultado de um job assíncrono (ex.: relatório) pelo `job_id` retornado por outra tool. |
| `cigam_estoque` | Posição atual de estoque (saldo por código de barras). |
| `cigam_contas_receber` | Lista contas a receber por período. |
| `cigam_contas_pagar` | Lista contas a pagar por período. |
| `cigam_caixa` | Lista fechamentos de caixa por período. |
| `cigam_lancamentos` | Lista lançamentos financeiros por período. |
| `cigam_fornecedores` | Lista/pesquisa fornecedores cadastrados. |
| `cigam_consulta` | Consulta genérica ao gateway do CIGAM (ObterCarga) para listas auxiliares (planos de conta, formas de pagamento, marcas, etc.). |

---

## Pricing

See [docs/precos.md](docs/precos.md) (PT-BR).

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_cigam` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
