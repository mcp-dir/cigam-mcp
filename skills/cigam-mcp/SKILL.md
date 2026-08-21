---
name: cigam-mcp
description: Skill da REST API do CIGAM na MCP.AI: 22 endpoints em /api/cigam. ERP CIGAM (gestão para indústria, varejo e franquias) por captura de sessão com a sua autorização. Como o CIGAM não tem API pública, você informa a sua Chave de acesso, usuário e senha e a plataforma entra na sua conta para ler os seus próprios dados, na mesma API que o portal CIGAM usa. Somente leitura: vendas, notas fiscais, contas a pagar e a receber, fechamento de caixa, lançamentos financeiros e fornecedores. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# CIGAM — REST API skill

Você tem acesso à **CIGAM** REST API na MCP.AI.

> ERP CIGAM (gestão para indústria, varejo e franquias) por captura de sessão com a sua autorização. Como o CIGAM não tem API pública, você informa a sua Chave de acesso, usuário e senha e a plataforma entra na sua conta para ler os seus próprios dados, na mesma API que o portal CIGAM usa. Somente leitura: vendas, notas fiscais, contas a pagar e a receber, fechamento de caixa, lançamentos financeiros e fornecedores.

## Base URL

```
https://api.mcp.ai/api/cigam
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/cigam/caixa \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"loja":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/cigam/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (22)

#### `cigam_caixa`

Lista fechamentos de caixa por período. _(POST /api/cigam/caixa)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `numero_caixa` | string | Não | Filtra por número do caixa. |
| `situacao` | string | Não | Situação ("A"=ativo/aberto, etc.). Default conforme a tela. |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_compras`

Compras de uma loja por período (notas fiscais de entrada do tipo Compra). _(POST /api/cigam/compras)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_consulta`

Consulta genérica ao gateway do CIGAM (ObterCarga) para listas auxiliares (planos de conta, formas de pagamento, marcas, etc.). _(POST /api/cigam/consulta)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `guid` | string | Sim | Nome da consulta. Ex.: OBJ_SELECT_LOJAS, OBJ_SELECT_PLANOCONTAS, OBJ_SELECT_FORMAPGTO_CPAGAR, OBJ_SELECT_MARCA. |
| `params` | string | Não | Parâmetros como JSON string. Ex.: {"TIPOCONTA":"1"}. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_contas_pagar`

Lista contas a pagar por período. _(POST /api/cigam/contas/pagar)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `numero_nf` | string | Não | Filtra por número da nota fiscal. |
| `duplicata` | string | Não | Filtra por número da duplicata. |
| `cod_fornecedor` | string | Não | Filtra por código do fornecedor. |
| `cod_plano_contas` | string | Não | Filtra por código do plano de contas. |
| `situacao` | string | Não | Situação ("A"=ativo/aberto, etc.). Default conforme a tela. |
| `tipo_data` | string | Não | Tipo da data filtrada: "V"=vencimento, "L"=lançamento, "B"=baixa (varia por tela). |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_contas_receber`

Lista contas a receber por período. _(POST /api/cigam/contas/receber)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Não | Código da loja/empresa (ex.: "Z136"). Opcional. Veja cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `cod_cliente` | string | Não | Filtra por código do cliente. |
| `situacao` | string | Não | Situação ("A"=ativo/aberto, etc.). Default conforme a tela. |
| `tipo_data` | string | Não | Tipo da data filtrada: "V"=vencimento, "L"=lançamento, "B"=baixa (varia por tela). |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_devolucoes`

Devoluções de uma loja por período (notas fiscais com movimento de devolução, entrada e saída). _(POST /api/cigam/devolucoes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_estoque`

Posição atual de estoque (saldo por código de barras). _(POST /api/cigam/estoque)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `codigo_barra` | string | Não | Código de barras para consultar o saldo de um produto específico. |
| `limit` | integer | Não | Quantos itens com saldo retornar na amostra (default 100, máx 1000). |
| `aguardar_segundos` | integer | Não | Quanto esperar inline antes de devolver um job_id (default 25). |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_fluxo_caixa`

Fluxo de caixa projetado de uma loja por período: total a receber (contas a receber em aberto) vs total a pagar (contas a pagar), e o saldo projetado. _(POST /api/cigam/fluxo/caixa)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_formas_pagamento`

Mix de formas de recebimento de uma loja por período: total recebido por forma de pagamento, por bandeira de cartão e por adquirente (maquininha). _(POST /api/cigam/formas/pagamento)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Não | Código da loja/empresa (ex.: "Z136"). Opcional. Veja cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_fornecedores`

Lista/pesquisa fornecedores cadastrados. _(POST /api/cigam/fornecedores)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `cnpj` | string | Não | Filtra por CNPJ (vazio = todos). |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_inadimplencia`

Contas a receber vencidas e ainda em aberto (inadimplência). _(POST /api/cigam/inadimplencia)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_job`

Busca o resultado de um job assíncrono (ex.: relatório) pelo `job_id` retornado por outra tool. _(POST /api/cigam/job)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `job_id` | string | Sim | O job_id retornado por uma tool assíncrona (ex.: cigam_relatorio). |
| `aguardar_segundos` | integer | Não | Quanto esperar inline (default 25). |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |
| `job_ids` | string[] | Não | Bulk mode: multiple values for job_id |

#### `cigam_lancamentos`

Lista lançamentos financeiros por período. _(POST /api/cigam/lancamentos)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `cod_plano_contas` | string | Não | Filtra por código do plano de contas. |
| `tipo_conta` | string | Não | Tipo da conta: "D"=débito, "C"=crédito. Default "D". |
| `tipo_data` | string | Não | Tipo da data filtrada: "V"=vencimento, "L"=lançamento, "B"=baixa (varia por tela). |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_list_accounts`

Lista as contas CIGAM conectadas a este install — id, label (instância/usuário). _(POST /api/cigam/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_listar_lojas`

Lista as lojas/empresas que a conta enxerga (código, nome, CNPJ). _(POST /api/cigam/listar/lojas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_notas_fiscais`

Lista notas fiscais de uma loja por período. _(POST /api/cigam/notas/fiscais)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `numero_nf` | integer | Não | Filtra por um número de NF específico. |
| `referencia` | string | Não | Filtra por referência. |
| `status` | integer[] | Não | Status da NF: 1=Confirmada, 3=Em cadastro, 2=Denegada, 4=Cancelada. Default [1,3]. |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_ranking_clientes`

Ranking de clientes por valor vendido no período (agrupa as vendas por destinatário/CNPJ-CPF). _(POST /api/cigam/ranking/clientes)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `top` | integer | Não | Quantos clientes retornar (default 20, máx 200). |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_relatorio`

Gera um relatório do CIGAM (operação LENTA, ~2 min, produz um arquivo Excel). _(POST /api/cigam/relatorio)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `report_id` | string | Sim | Id do relatório no formato REL_<numero>. Ex.: "REL_201" (Vendas por Período), "REL_610" (CSV posição atual de estoque). |
| `filtros` | string | Não | Filtros do relatório como JSON. Ex.: {"filtro_1":"01/06/2026","filtro_2":"30/06/2026"} (datas DD/MM/YYYY). |
| `aguardar_segundos` | integer | Não | Quanto esperar inline antes de devolver um job_id (default 25). |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |
| `report_ids` | string[] | Não | Bulk mode: multiple values for report_id |

#### `cigam_resultado`

Resultado gerencial simplificado de uma loja por período: receita (vendas faturadas líquidas de devolução) menos despesas (lançamentos financeiros por plano de contas), com o detalhe das despesas por _(POST /api/cigam/resultado)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_vendas`

Vendas de uma loja por período (notas fiscais de saída do tipo Venda). _(POST /api/cigam/vendas)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `page` | integer | Não | Página da saída (default 1). |
| `limit` | integer | Não | Itens por página (default 100, máx 1000). O CIGAM não pagina no servidor; paginamos aqui. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_vendas_por_dia`

Série de vendas por dia no período (quantidade e valor por data) + resumo com total e ticket médio. _(POST /api/cigam/vendas/por/dia)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

#### `cigam_vendas_resumo`

Panorama do período numa loja: totais de vendas, compras e devoluções (quantidade e valor de cada). _(POST /api/cigam/vendas/resumo)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `loja` | string | Sim | Código da loja/empresa (ex.: "Z136"). Obrigatório aqui. Descubra os códigos com cigam_listar_lojas. |
| `data_inicial` | string | Não | Data inicial no formato YYYY-MM-DD. Default: 30 dias atrás. |
| `data_final` | string | Não | Data final no formato YYYY-MM-DD. Default: hoje. |
| `account` | string | Não | Quando há múltiplas contas CIGAM conectadas: id/label da conexão. Veja cigam_list_accounts. |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_cigam` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
