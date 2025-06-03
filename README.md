# A3_BancoDados_SQL_HenriqueDayrell

##  Descrição do Projeto
Sistema de gerenciamento de carteiras de criptomoedas chamado **CryptoWallet Pro**, com foco em controle de usuários, carteiras, criptomoedas e transações.

---

##  Estrutura do Banco

### Tabela `Usuário`
- `usuario_id`: Identificador do usuário (PK)
- `nome`: Nome do usuário
- `email`: Email único
- `criado_em`: Timestamp automático de criação

### Tabela `Carteira`
- `carteira_id`: ID da carteira (PK)
- `usuario_id`: FK do dono da carteira
- `nome`: Nome da carteira
- `saldo`: Saldo atual (padrão 0.0)
- `criado_em`: Timestamp automático de criação

### Tabela `Criptomoeda`
- `cripto_id`: ID da criptomoeda (PK)
- `nome`: Nome completo da moeda
- `simbolo`: Abreviação (ex: BTC)

### Tabela `Transação`
- `transacao_id`: ID da transação (PK)
- `carteira_id`: FK da carteira
- `cripto_id`: FK da criptomoeda
- `quantidade`: Quantia comprada ou vendida
- `valor_total`: Valor em moeda local (BRL, por exemplo)
- `data_transacao`: Data e hora da transação

---

## Como Executar

1. Acesse [DB Fiddle](https://www.db-fiddle.com)
2. Selecione **MySQL 8.0**
3. Cole o script completo no editor
4. Clique em **Build Schema**, depois **Run**
5. Veja os resultados e consultas funcionando!

📎 **Link para o DB Fiddle**:  

---

## Consultas de Verificação

### A) Transações da Ana Silva

```sql
SELECT t.data_transacao, c.simbolo, t.quantidade, t.valor_total
FROM Transacao AS t
JOIN Carteira AS w ON t.carteira_id = w.carteira_id
JOIN Usuario AS u ON w.usuario_id = u.usuario_id
JOIN Criptomoeda AS c ON t.cripto_id = c.cripto_id
WHERE u.usuario_id = 1
ORDER BY t.data_transacao;
```

### B) Total investido por Carteira

```sql
SELECT w.nome AS carteira, SUM(t.valor_total) AS total_investido
FROM Transacao AS t
JOIN Carteira AS w ON t.carteira_id = w.carteira_id
GROUP BY w.carteira_id;
```
### C) Quantidade total de cada Criptomoeda

```sql
SELECT c.simbolo, SUM(t.quantidade) AS total_quantidade
FROM Transacao AS t
JOIN Criptomoeda AS c ON t.cripto_id = c.cripto_id
GROUP BY c.cripto_id;
```

---

Autor Henrique Paulino  
Curso: Análise e Desenvolvimento de Sistemas  
UniBH – 2025  
