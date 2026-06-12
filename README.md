# Guia de Fundamentos: Linguagem SQL

Este repositório consolida os conceitos fundamentais, estruturas e comandos práticos da Linguagem SQL, servindo como um guia prático e rápido de consulta.

---

## 1. Introdução ao SQL
* **O que é:** SQL significa Linguagem de Consulta Estruturada (*Structured Query Language*) e frequentemente é pronunciada como "SeQuel".
* **Função:** É utilizado para interagir com dados armazenados em bancos de dados, permitindo a execução de cálculos complexos em grandes conjuntos de dados.
* **Por que aprender?** A linguagem permite a comunicação direta com sistemas de dados e possui alta demanda no mercado para diversas carreiras.
* **Padrão de Mercado:** É o padrão da indústria e se integra perfeitamente com ferramentas corporativas como Power BI, Tableau, Kafka, Spark e Synapse.

---

## 2. Sistema de Gerenciamento de Banco de Dados (SGBD / DBMS)
Um DBMS atua como a interface entre o usuário e o banco de dados propriamente dito. Geralmente, são hospedados em um servidor local ou na nuvem e funcionam 24/7. Aplicativos e ferramentas de BI enviam consultas SQL ao DBMS para recuperar e gerenciar dados.

**Tipos de Bancos de Dados:**
* **Relacional:** Microsoft SQL Server, MySQL, PostgreSQL, Amazon Redshift.
* **Documento:** MongoDB.
* **Grafo:** Neo4j.
* **Chave-Valor:** Redis, Amazon DynamoDB.
* **Base de Coluna:** Apache Cassandra.

---

## 3. Estrutura e Componentes de um Banco de Dados Relacional
A organização desses bancos segue uma estrutura hierárquica:

* **Servidor:** O host principal que contém um ou mais bancos de dados.
* **Banco de Dados:** Contêiner de alto nível para os dados.
* **Esquema (Schema):** Agrupamentos lógicos dentro de um banco.
* **Tabela:** Onde os dados são armazenados fisicamente.
  * **Colunas:** Categorias verticais definindo os tipos de dados.
  * **Linhas:** Registros horizontais individuais.
* **Célula:** Uma unidade única de dado na interseção exata de uma linha e coluna.

### Chaves de Identificação e Relacionamento

* **Chave Primária (Primary Key - PK):** O identificador único para cada registro dentro de uma tabela.
* **Chave Estrangeira (Foreign Key - FK):** Um campo de uma tabela que aponta para a chave primária de outra tabela. Ela serve para criar o relacionamento entre tabelas e ligar uma à outra. O uso de chaves estrangeiras garante a integridade dos dados, evita inconsistências e impede a existência de registros "órfãos" (sem relação real).

### Tipos de Dados Comuns

* **Numéricos:** `INT` e `DECIMAL`.
* **Texto/String:** `CHAR` e `VARCHAR`.
* **Data e Hora:** `DATE` e `TIME`.
* **Booleanos:** `BIT` ou `BOOLEAN`.
* **Grandes Objetos:** `BLOB`, `TEXT` e `CLOB`.

---

## 4. Normalização de Dados
Normalizar um banco de dados é organizar as informações para que cada dado exista apenas uma vez, evitando repetição, erros e bagunça nas tabelas.

### As Formas Normais

* **Forma Não Normalizada (UNF):** Todos os dados estão misturados em uma única tabela, com grupos e informações repetidas.
* **Primeira Forma Normal (1FN):** Os campos devem ser atômicos, ou seja, possuir um único valor por célula.
* **Segunda Forma Normal (2FN):** A tabela deve estar na 1FN. Removemos as dependências parciais, fazendo com que cada entidade passe a ter sua própria tabela e sua própria chave primária.
* **Terceira Forma Normal (3FN):** A tabela deve estar na 2FN. Removemos as dependências transitivas, garantindo que campos não-chave dependam exclusivamente da chave primária.

> **Resultado da Normalização:** O banco passa a ter ausência de redundância, relacionamentos claros (através de chaves estrangeiras) e manutenção facilitada, tornando-se mais eficiente e confiável.

---

## 5. As Subdivisões de Comandos SQL

* **DDL (Data Definition Language):** Criar, alterar ou excluir estruturas do banco.
* **DQL (Data Query Language):** Recuperar e consultar dados.
* **DML (Data Manipulation Language):** Inserir, atualizar e remover dados.
* **DCL (Data Control Language):** Gerenciar permissões e acessos.
* **TCL (Transaction Control Language):** Controlar transações e consistência dos dados.

---

## 6. DDL: Definindo o "Esqueleto" do Banco de Dados

Gerencia a estrutura do banco de dados através de três ações principais:

* `CREATE`: Constrói novos objetos (bancos, tabelas, views, procedures ou schemas).
* `ALTER`: Modifica a estrutura de um objeto existente.
* `DROP`: Exclui permanentemente um objeto e todos os registros (altamente destrutivo).

### Exemplo

```sql
CREATE TABLE Clientes (
    Id INT PRIMARY KEY,
    Nome VARCHAR(100),
    Email VARCHAR(150)
);
```

---

## 7. DML: Manipulando os Dados

A DML permite gerenciar o conteúdo real armazenado nas tabelas. Trabalhamos com três comandos principais:

| Comando | Ação | Efeito nos Dados |
| :--- | :--- | :--- |
| **INSERT** | Adicionar | Novas linhas são criadas. |
| **UPDATE** | Editar | Valores existentes são alterados. |
| **DELETE** | Remover | Linhas selecionadas são apagadas. |

### Exemplos

```sql
INSERT INTO Clientes (Id, Nome)
VALUES (1, 'Maria');
```

```sql
UPDATE Clientes
SET Nome = 'Maria Silva'
WHERE Id = 1;
```

```sql
DELETE FROM Clientes
WHERE Id = 1;
```

---

## 8. DQL: Consultando e Recuperando Dados

O comando principal para buscar dados é o `SELECT`.

### Anatomia de uma Declaração SQL

* **Comentários (`--`)**: Documentam o código.
* **Palavras-chave:** Reservadas e com significado especial.
* **Cláusulas:** Blocos que constroem a instrução.
* **Funções:** Ferramentas internas que transformam dados.
* **Identificadores:** Nomes de objetos como tabelas ou colunas.
* **Operadores / Literais:** Usados para comparações e valores constantes.

### Filtros e Organização

* `WHERE`: Filtra registros com condições específicas.
* `ORDER BY`: Ordena resultados.
* `DISTINCT`: Remove duplicidades.
* `TOP` / `LIMIT`: Limita a quantidade de linhas retornadas.
* `AS`: Define apelidos para colunas ou tabelas.

### Ordem Lógica de Processamento

1. `FROM`
2. `WHERE`
3. `SELECT`
4. `ORDER BY`

---

## 9. Métodos de Combinação de Dados

Permitem unir informações de múltiplas tabelas ou consultas.

### JOINS (Adição de Colunas - Horizontal)

* **INNER JOIN:** Apenas correspondências.
* **LEFT JOIN:** Tudo da esquerda e correspondências da direita.
* **RIGHT JOIN:** Tudo da direita e correspondências da esquerda.
* **FULL JOIN:** Todos os registros de ambas as tabelas.

### Exemplo

```sql
SELECT
    A.Nome,
    B.Pais
FROM TabelaA A
INNER JOIN TabelaB B
ON A.Id = B.Id;
```

---

## 10. Operadores SET (Adição de Linhas - Vertical)

Empilham resultados de consultas compatíveis.

* `UNION`: Combina e remove duplicados.
* `UNION ALL`: Combina mantendo duplicados.
* `EXCEPT` / `MINUS`: Retorna apenas registros exclusivos da primeira consulta.
* `INTERSECT`: Retorna apenas registros comuns.

### Exemplo

```sql
SELECT Nome FROM Clientes
UNION
SELECT Nome FROM Funcionarios;
```

---

## 11. Funções de Linha Única (Single Row Functions)

Funções que retornam um único valor por linha.

### Funções de Texto

```sql
SELECT
    UPPER(nome),
    LOWER(nome),
    TRIM(nome),
    REPLACE(nome,'a','x')
FROM clientes;
```

### Funções de Data

```sql
SELECT
    YEAR(data_venda),
    MONTH(data_venda),
    DAY(data_venda)
FROM vendas;
```

### Tratamento de NULL

```sql
SELECT
    ISNULL(nome,'Não informado'),
    COALESCE(nome,sobrenome,'N/A')
FROM clientes;
```

### Lógica Condicional

```sql
SELECT
    nome,
    CASE
        WHEN salario > 5000 THEN 'Alto'
        WHEN salario > 2000 THEN 'Médio'
        ELSE 'Baixo'
    END AS nivel_salario
FROM funcionarios;
```

---

## 12. Funções de Agregação e GROUP BY

Funções que retornam um único valor para um conjunto de linhas.

### Funções Principais

```sql
SELECT
    COUNT(*),
    SUM(valor),
    AVG(valor),
    MAX(valor),
    MIN(valor)
FROM vendas;
```

### GROUP BY

```sql
SELECT
    regiao,
    SUM(valor) AS total_vendas
FROM vendas
GROUP BY regiao;
```

### HAVING

Utilizado para filtrar grupos após a agregação.

```sql
SELECT
    regiao,
    SUM(valor) AS total_vendas
FROM vendas
GROUP BY regiao
HAVING SUM(valor) > 10000;
```

---

## 13. Views

Uma View é uma tabela virtual criada a partir de uma consulta SQL. Ela não armazena dados fisicamente (na maioria dos SGBDs), apenas o resultado da consulta.

### Vantagens

* Simplifica consultas complexas.
* Aumenta a segurança dos dados.
* Facilita a reutilização de consultas.

### Exemplo

```sql
CREATE VIEW vw_ClientesAtivos AS
SELECT
    Id,
    Nome,
    Email
FROM Clientes
WHERE Ativo = 1;
```

Consulta da View:

```sql
SELECT * FROM vw_ClientesAtivos;
```

---

## 14. Functions

São rotinas que recebem parâmetros e retornam um valor ou tabela.

### Características

* Reutilização de lógica.
* Retorno obrigatório.
* Podem ser utilizadas dentro de consultas.

### Exemplo

```sql
CREATE FUNCTION fn_CalcularDesconto
(
    @Valor DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)
AS
BEGIN
    RETURN @Valor * 0.9;
END;
```

Uso:

```sql
SELECT dbo.fn_CalcularDesconto(1000);
```

---

## 15. Stored Procedures (Procedimentos Armazenados)

São blocos de código SQL armazenados no banco de dados para execução posterior.

### Vantagens

* Reutilização de código.
* Melhor desempenho.
* Centralização das regras de negócio.

### Exemplo

```sql
CREATE PROCEDURE sp_ListarClientes
AS
BEGIN
    SELECT *
    FROM Clientes;
END;
```

Execução:

```sql
EXEC sp_ListarClientes;
```

---

## 16. Triggers

São procedimentos executados automaticamente quando determinados eventos ocorrem em uma tabela.

### Eventos Comuns

* `INSERT`
* `UPDATE`
* `DELETE`

### Aplicações

* Auditoria.
* Logs.
* Validação de regras de negócio.

### Exemplo

```sql
CREATE TRIGGER trg_LogClientes
ON Clientes
AFTER INSERT
AS
BEGIN
    PRINT 'Novo cliente cadastrado';
END;
```

---

## 17. DCL (Data Control Language)

Responsável pelo controle de acesso aos objetos do banco.

### Principais Comandos

* `GRANT`: Concede permissões.
* `REVOKE`: Remove permissões.

### Exemplo

```sql
GRANT SELECT
ON Clientes
TO UsuarioAnalista;
```

```sql
REVOKE SELECT
ON Clientes
FROM UsuarioAnalista;
```

### Objetivo

Garantir segurança e controle sobre quem pode visualizar ou modificar informações.

---

## 18. TCL (Transaction Control Language)

Controla transações, garantindo consistência e integridade dos dados.

### Conceito de Transação

Uma transação é um conjunto de operações executadas como uma única unidade lógica de trabalho.

### Principais Comandos

| Comando | Função |
|----------|----------|
| `BEGIN TRANSACTION` | Inicia uma transação |
| `COMMIT` | Confirma as alterações |
| `ROLLBACK` | Desfaz as alterações |
| `SAVEPOINT` | Cria um ponto intermediário para retorno |

### Exemplo

```sql
BEGIN TRANSACTION;

UPDATE Contas
SET Saldo = Saldo - 100
WHERE Id = 1;

UPDATE Contas
SET Saldo = Saldo + 100
WHERE Id = 2;

COMMIT;
```

### Exemplo com ROLLBACK

```sql
BEGIN TRANSACTION;

UPDATE Produtos
SET Estoque = Estoque - 10
WHERE Id = 1;

ROLLBACK;
```

### Relação com ACID

As transações são responsáveis por garantir as propriedades ACID:

* **Atomicidade:** Tudo acontece ou nada acontece.
* **Consistência:** Mantém regras e integridade.
* **Isolamento:** Transações não interferem umas nas outras.
* **Durabilidade:** Alterações confirmadas permanecem salvas mesmo após falhas.

---

## 19. Resumo Geral das Categorias SQL

| Categoria | Objetivo | Principais Comandos |
|------------|------------|--------------------|
| DDL | Estrutura | CREATE, ALTER, DROP |
| DML | Manipulação de Dados | INSERT, UPDATE, DELETE |
| DQL | Consulta de Dados | SELECT |
| DCL | Controle de Acesso | GRANT, REVOKE |
| TCL | Controle de Transações | COMMIT, ROLLBACK, SAVEPOINT |

---

## Conclusão

* **DDL** define a estrutura do banco.
* **DML** manipula os dados armazenados.
* **DQL** consulta informações.
* **DCL** controla permissões e segurança.
* **TCL** garante consistência através de transações.
* **Views** simplificam consultas complexas.
* **Functions** encapsulam cálculos e regras reutilizáveis.
* **Stored Procedures** automatizam processos e centralizam lógica de negócio.
* **Triggers** executam ações automáticas em resposta a eventos.
