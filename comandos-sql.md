## Comandos sql - referências

## Modelagem Física com comandos DDL

## Criar banco de dados

CREATE DATABASE vendas CHARACTER SET utf8mb4

## Criar tabela fabricantes

```SQL
CREATE TABLE fabricantes(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL
);
```
### Vizualizar detalhes estruturais da tabela

```sql
DESC fabricantes;
```

### Criar tabela de produtos

```sql
CREATE TABLE produtos(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL,
    descricao TEXT(500) NULL,
    preco DECIMAL(6,2) NOT NULL,
    fabricante_id INT NOT NULL
);
```

### Criação do relacionamento entre as tabelas (chave estrangeira)

```sql
ALTER TABLE produtos
    -- CONSTRAINT/RESTRIÇÃO indicando o nome do relacionamento
    ADD CONSTRAINT fk_produtos_fabricantes

    -- Criando a chave-estrangera (fabricante id) que 
    -- aponta para a chave-primária (id) de outra tabela(fabricante)
    FOREIGN KEY (fabricante_id) REFERENCES fabricantes(id);
```

### Exemplos de alterações estruturais  na tabela

### Renomear tabela

```sql
ALTER TABLE fabricantes RENAME TO fornecedores;
ALTER TABLE fornecedores RENAME TO  fabricantes;
```

### Modificar colunas

```sql
ALTER TABLE produtos
    MODIFY COLUMN preco DECIMAL(6,2) NOT NULL;
```

### RENOMEAR COLUNAS

```sql
ALTER TABLE fabricantes
    CHANGE nome nome_do_fabricantes VARCHAR(20) NOT NULL;

ALTER TABLE fabricantes
    CHANGE nome_do_fabricantes nome VARCHAR(45) NOT NULL;
```

### Adicionar coluna
```sql
ALTER TABLE produtos
    ADD quantidade INT NULL AFTER preco;
```