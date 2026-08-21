# Ferramentas

CIGAM expõe 22 ferramentas.

### 1. `cigam_list_accounts`
**Input**: `account` (opcional)

Lista as contas CIGAM conectadas a este install — id, label (instância/usuário).

### 2. `cigam_listar_lojas`
**Input**: `account` (opcional)

Lista as lojas/empresas que a conta enxerga (código, nome, CNPJ).

### 3. `cigam_notas_fiscais`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `numero_nf` (opcional), `referencia` (opcional), `status` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Lista notas fiscais de uma loja por período.

### 4. `cigam_vendas`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Vendas de uma loja por período (notas fiscais de saída do tipo Venda).

### 5. `cigam_compras`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Compras de uma loja por período (notas fiscais de entrada do tipo Compra).

### 6. `cigam_devolucoes`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Devoluções de uma loja por período (notas fiscais com movimento de devolução, entrada e saída).

### 7. `cigam_vendas_resumo`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `account` (opcional)

Panorama do período numa loja: totais de vendas, compras e devoluções (quantidade e valor de cada).

### 8. `cigam_fluxo_caixa`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `account` (opcional)

Fluxo de caixa projetado de uma loja por período: total a receber (contas a receber em aberto) vs total a pagar (contas a pagar), e o saldo projetado.

### 9. `cigam_ranking_clientes`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `top` (opcional), `account` (opcional)

Ranking de clientes por valor vendido no período (agrupa as vendas por destinatário/CNPJ-CPF).

### 10. `cigam_vendas_por_dia`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `account` (opcional)

Série de vendas por dia no período (quantidade e valor por data) + resumo com total e ticket médio.

### 11. `cigam_inadimplencia`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Contas a receber vencidas e ainda em aberto (inadimplência).

### 12. `cigam_resultado`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `account` (opcional)

Resultado gerencial simplificado de uma loja por período: receita (vendas faturadas líquidas de devolução) menos despesas (lançamentos financeiros por plano de contas), com o detalhe das despesas por categoria.

### 13. `cigam_formas_pagamento`
**Input**: `loja` (opcional), `data_inicial` (opcional), `data_final` (opcional), `account` (opcional)

Mix de formas de recebimento de uma loja por período: total recebido por forma de pagamento, por bandeira de cartão e por adquirente (maquininha).

### 14. `cigam_relatorio`
**Input**: `report_id`, `filtros` (opcional), `aguardar_segundos` (opcional), `account` (opcional), `report_ids` (opcional)

Gera um relatório do CIGAM (operação LENTA, ~2 min, produz um arquivo Excel).

### 15. `cigam_job`
**Input**: `job_id`, `aguardar_segundos` (opcional), `account` (opcional), `job_ids` (opcional)

Busca o resultado de um job assíncrono (ex.: relatório) pelo `job_id` retornado por outra tool.

### 16. `cigam_estoque`
**Input**: `codigo_barra` (opcional), `limit` (opcional), `aguardar_segundos` (opcional), `account` (opcional)

Posição atual de estoque (saldo por código de barras).

### 17. `cigam_contas_receber`
**Input**: `loja` (opcional), `data_inicial` (opcional), `data_final` (opcional), `cod_cliente` (opcional), `situacao` (opcional), `tipo_data` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Lista contas a receber por período.

### 18. `cigam_contas_pagar`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `numero_nf` (opcional), `duplicata` (opcional), `cod_fornecedor` (opcional), `cod_plano_contas` (opcional), `situacao` (opcional), `tipo_data` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Lista contas a pagar por período.

### 19. `cigam_caixa`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `numero_caixa` (opcional), `situacao` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Lista fechamentos de caixa por período.

### 20. `cigam_lancamentos`
**Input**: `loja`, `data_inicial` (opcional), `data_final` (opcional), `cod_plano_contas` (opcional), `tipo_conta` (opcional), `tipo_data` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Lista lançamentos financeiros por período.

### 21. `cigam_fornecedores`
**Input**: `cnpj` (opcional), `page` (opcional), `limit` (opcional), `account` (opcional)

Lista/pesquisa fornecedores cadastrados.

### 22. `cigam_consulta`
**Input**: `guid`, `params` (opcional), `account` (opcional)

Consulta genérica ao gateway do CIGAM (ObterCarga) para listas auxiliares (planos de conta, formas de pagamento, marcas, etc.).

## Prompts de exemplo

```
Quanto a loja Z136 vendeu neste mês?
Quais contas a pagar vencem nos próximos 7 dias?
Mostre o fechamento de caixa da última semana
```
