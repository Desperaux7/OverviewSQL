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

* **DDL (Data Definition Language):** Criar, alterar ou excluir a estrutura.
* **DQL (Data Query Language):** Recuperar e consultar dados.
* **DML (Data Manipulation Language):** Gerenciar e manipular os dados.
* **DCL (Data Control Language):** Gerenciar permissões (`GRANT`, `REVOKE`).
* **TCL (Transaction Control Language):** Gerenciar transações (`COMMIT`, `ROLLBACK`).

---

## 6. DDL: Definindo o "Esqueleto" do Banco de Dados
Gerencia a estrutura do banco de dados através de três ações principais:

* `CREATE`: Constrói novos objetos (bancos, tabelas ou schemas).
* `ALTER`: Modifica a estrutura de um objeto existente.
* `DROP`: Exclui permanentemente um objeto e todos os registros (altamente destrutivo).

---

## 7. DML: Manipulando os Dados
A DML permite gerenciar o conteúdo real armazenado nas tabelas. Trabalhamos com três comandos principais:

| Comando | Ação | Efeito nos Dados |
| :--- | :--- | :--- |
| **INSERT** | Adicionar | Novas linhas são criadas. Pode ser feito manualmente (`VALUES`) ou copiando de outra tabela (`INSERT INTO ... SELECT`). |
| **UPDATE** | Editar | Valores existentes são alterados. Sempre utilize `WHERE` para evitar atualização em massa. |
| **DELETE** | Remover | Linhas selecionadas são apagadas. Também exige `WHERE` para filtrar linhas específicas. |

---

## 8. DQL: Consultando e Recuperando Dados
O comando principal para buscar dados é o `SELECT`.

### Anatomia de uma Declaração SQL

* **Comentários (`--`):** Documentam o código.
* **Palavras-chave:** Reservadas e com significado especial.
* **Cláusulas:** Blocos que constroem a instrução.
* **Funções:** Ferramentas internas que transformam dados.
* **Identificadores:** Nomes de objetos como tabelas ou colunas.
* **Operadores / Literais:** Usados para comparações e valores constantes.

### Filtros e Organização

* `WHERE`: Filtra registros com condições específicas.
* `ORDER BY`: Ordena resultados de forma ascendente ou descendente.
* `DISTINCT`: Remove resultados duplicados.
* `TOP` / `LIMIT`: Especifica o número de registros retornados.
* **Aliases (`AS`):** Define nomes temporários para colunas ou tabelas, tornando os resultados mais legíveis.

### Ordem Lógica de Processamento

O banco de dados não executa as cláusulas na ordem escrita. A execução lógica padrão é:

1. `FROM`
2. `WHERE`
3. `SELECT`
4. `ORDER BY`

---

## 9. Métodos de Combinação de Dados
Permitem unir informações de múltiplas tabelas ou consultas.

### JOINS (Adição de Colunas - Horizontal)

Conectamos tabelas lateralmente através de uma coluna comum, geralmente a chave primária e estrangeira.

* **Inner Join:** Retorna apenas o que existe correspondência em ambas as tabelas.
* **Left Join:** Mantém tudo da tabela à esquerda e traz o que houver de correspondência da tabela à direita.
* **Right Join:** Mantém tudo da tabela à direita e traz o que houver de correspondência da tabela à esquerda.
* **Full Join:** Traz todos os dados de ambos os lados, independentemente de haver correspondência.

### Exemplo de JOIN

```sql
SELECT 
    TabelaA.Nome, 
    TabelaB.Pais 
FROM TabelaA 
INNER JOIN TabelaB ON TabelaA.id = TabelaB.id; -- Especificando a relação
```

---

## 10. Operadores SET (Adição de Linhas - Vertical)
Empilhamos resultados de consultas diferentes, desde que ambas tenham exatamente a mesma estrutura de colunas.

UNION: Combina os resultados e remove os registros duplicados.
UNION ALL: Combina tudo, incluindo os duplicados (é uma operação mais rápida).
EXCEPT / MINUS: Mostra o que existe exclusivamente no primeiro conjunto, mas não no segundo.
INTERSECT: Mostra apenas os registros que são comuns a ambos os conjuntos.

Exemplo de Operador SET:

```sql
SELECT Nome FROM Clientes
UNION
SELECT Nome FROM Funcionarios;
```
