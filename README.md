#  Guia de Fundamentos: Linguagem SQL

Este repositório consolida os conceitos fundamentais, estruturas e comandos práticos da Linguagem SQL, servindo como um guia prático e rápido de consulta.

---

##  1. Introdução ao SQL

- **O que é:** SQL significa Linguagem de Consulta Estruturada (*Structured Query Language*) e frequentemente é pronunciada como "SeQuel".
- **Função:** É utilizado para interagir com dados armazenados em bancos de dados, permitindo a execução de cálculos complexos (como encontrar gastos totais) em grandes conjuntos de dados.
- **Por que aprender?** A linguagem permite a comunicação direta com sistemas de dados e possui alta demanda no mercado para diversas carreiras, como Desenvolvedores de Software, Analistas de Dados, Cientistas de Dados e Engenheiros de Dados.
- **Padrão de Mercado:** É o padrão da indústria e se integra perfeitamente com ferramentas corporativas como Power BI, Tableau, Kafka, Spark e Synapse.

---

##  2. Sistema de Gerenciamento de Banco de Dados (SGBD / DBMS)

- Um DBMS atua como a interface entre o usuário e o banco de dados propriamente dito.
- Geralmente, os bancos de dados são hospedados em um servidor local ou na nuvem e funcionam 24/7 para garantir que os dados estejam sempre disponíveis e acessíveis.
- Aplicativos (APPs) e ferramentas de BI enviam consultas SQL ao DBMS para recuperar e gerenciar dados.

###  Tipos de Bancos de Dados

- **Relacional:** Exemplos incluem Microsoft SQL Server, MySQL, PostgreSQL e Amazon Redshift.
- **Documento:** Exemplo: MongoDB.
- **Grafo:** Exemplo: Neo4j.
- **Chave-Valor:** Exemplos incluem Redis e Amazon DynamoDB.
- **Base de Coluna:** Exemplo: Apache Cassandra.

---

##  3. Estrutura e Componentes de um Banco de Dados Relacional

A organização desses bancos segue uma estrutura hierárquica:

- **Servidor:** O host principal que contém um ou mais bancos de dados.
- **Banco de Dados:** Contêiner de alto nível para os dados (ex: "Vendas", "RH").
- **Esquema (Schema):** Agrupamentos lógicos dentro de um banco (ex: "Pedidos", "Clientes").
- **Tabela:** Onde os dados são armazenados fisicamente.  
  Contém:
  - **Colunas:** Categorias verticais definindo os tipos de dados.
  - **Linhas:** Registros horizontais individuais.  
  As tabelas são armazenadas como arquivos físicos no disco.
- **Célula:** Uma unidade única de dado na interseção exata de uma linha e coluna.
- **Chave Primária:** O identificador único para cada registro dentro de uma tabela.

###  Tipos de Dados Comuns

- **Numéricos:** `INT` (números inteiros) e `DECIMAL` (valores numéricos com frações).
- **Texto/String:** `CHAR` (strings de tamanho fixo) e `VARCHAR` (strings de tamanho variável).
- **Data e Hora:** `DATE` (formato YYYY-MM-DD) e `TIME` (formato HH:MM:SS).

---

##  4. As Subdivisões de Comandos SQL

A linguagem SQL é dividida em diferentes famílias de comandos para propósitos específicos:

- **DDL (Data Definition Language):** Criar, alterar ou excluir a estrutura do banco de dados.
- **DQL (Data Query Language):** Recuperar e consultar dados.
- **DML (Data Manipulation Language):** Gerenciar e manipular os dados dentro das tabelas.
- **DCL (Data Control Language):** Gerenciar permissões e controles de acesso (`GRANT`, `REVOKE`).
- **TCL (Transaction Control Language):** Gerenciar transações (`COMMIT`, `ROLLBACK`, `SAVEPOINT`).

---

##  5. DDL: Definindo o "Esqueleto" do Banco de Dados

Enquanto a DQL consulta dados e a DML manipula os dados, o DDL gerencia a estrutura do banco de dados através de três ações principais:

- **CREATE:** Constrói novos objetos (bancos de dados, tabelas ou schemas).
- **ALTER:** Modifica a estrutura (colunas e tipos de dados) de um objeto existente.
- **DROP:** Exclui permanentemente um objeto e todos os registros contidos nele (comando altamente destrutivo).

### Exemplos Práticos de DDL

-- Criando um banco de dados
CREATE DATABASE Sales;

-- Criando uma tabela com tipos de dados associados
CREATE TABLE Products (
  ProductID INT,
  ProductName VARCHAR(100),
  Price DECIMAL(10,2)
);

-- Adicionando uma nova coluna
ALTER TABLE Products ADD Category VARCHAR(50);

-- Removendo uma coluna
ALTER TABLE Products DROP COLUMN Price;

-- Excluindo a tabela permanentemente
DROP TABLE Products;

##  6. DML: Manipulando os Dados

A DML gerencia o conteúdo interno criado pela DDL. Trabalhamos com três comandos principais:

- **INSERT**: Adiciona novas linhas de dados à tabela.
- **UPDATE**: Modifica informações existentes. Sempre utilize WHERE para evitar atualização em massa.
- **DELETE**: Remove registros específicos. Também exige WHERE para evitar exclusão total da tabela.

### Exemplos Práticos de DML

-- Inserindo dados manualmente
INSERT INTO Products (ProductID, ProductName, Price) 
VALUES (1, 'Laptop', 1200.00);

-- Inserindo dados via SELECT
INSERT INTO TargetTable 
SELECT * FROM SourceTable 
WHERE condition;

-- Atualizando um registro
UPDATE table_name 
SET column1 = value1, column2 = value2 
WHERE condition;

-- Deletando um registro específico
DELETE FROM table_name 
WHERE condition;

## 7. DQL: Consultando e Recuperando Dados

O comando principal para buscar dados no SQL é o SELECT.

### Anatomia de uma Declaração SQL

Uma instrução SQL possui:

- Comentários (--)
- Palavras-chave
- Cláusulas
- Funções
- Identificadores
- Operadores
- Literais

### Estrutura Básica

SELECT column_name
FROM table_name;

### Filtros e Organização

- **WHERE**: Filtra registros.
- **ORDER BY**: Ordena resultados (ASC / DESC).
- **DISTINCT**: Remove duplicados.
- **TOP / LIMIT**: Limita número de registros.
- **Aliases** (AS): Define nomes temporários para colunas ou tabelas.

### Ordem Lógica de Processamento

O banco de dados não executa as cláusulas na ordem escrita. A ordem lógica padrão é:

1. FROM → Identifica a origem dos dados.
2. WHERE → Aplica filtros.
3. SELECT → Seleciona colunas após o filtro.
4. ORDER BY → Ordena o resultado final.
