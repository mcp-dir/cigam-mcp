# CIGAM

### CIGAM para Claude, ChatGPT e agentes de IA

ERP CIGAM (gestão para indústria, varejo e franquias) por captura de sessão com a sua autorização. Como o CIGAM não tem API pública, você informa a sua Chave de acesso, usuário e senha e a plataforma entra na sua conta para ler os seus próprios dados, na mesma API que o portal CIGAM usa. Somente leitura: vendas, notas fiscais, contas a pagar e a receber, fechamento de caixa, lançamentos financeiros e fornecedores.

- 📊 **22 ferramentas**
- ✏️ **Leitura e escrita**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `CIGAM` e **URL** `https://api.mcp.ai/p_cigam`.

### Cursor

[➕ Instalar CIGAM no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=cigam&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9jaWdhbSJ9)

### VS Code (Copilot Chat)

[➕ Instalar CIGAM no VS Code](vscode:mcp/install?name=cigam&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_cigam%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_cigam
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Quanto a loja Z136 vendeu neste mês?
Quais contas a pagar vencem nos próximos 7 dias?
Mostre o fechamento de caixa da última semana
```

---

## 22 ferramentas disponíveis

| Tool | Descrição |
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

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Planos a partir do tier grátis. Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Sub-processadores**: CIGAM (Senior Sistemas), o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_cigam`.


---

## Suporte

- 📧 [cigam@mcp.ai](mailto:cigam@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/cigam-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_cigam` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
