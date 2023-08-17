# Comandos para operações CRUD no Banco de dados

## Resumo

- C -> CREATE (inserir dados usando comando `INSERT`)
- R -> READ (ler dados usando comando `SELECT`)
- U -> UPDATE (atualizar dados usando comando `UPDATE`)
- D -> DELETE (excluir dados usando comando `DELETE`)

## INSERT

### Fabricantes

```sql
INSERT INTO fabricante(nome) VALUES('ASUS'); 

INSERT INTO fabricante(nome) VALUES('DELL'); 
INSERT INTO fabricante(nome) VALUES('APPLE'); 

INSERT INTO fabricante(nome) VALUES('LG'), ('SAMSUNG'), ('BRASTEMP'); 

INSERT INTO fabricante(nome) VALUES('POSITIVO'),('MICROSOFT');

```

### PRODUTOS

```sql
INSERT INTO produtos(nome, preco, descricao, quantidade, fabricante_id) VALUES('ULTRABOOK', 3500,'Equipamento de última geração cheio de recursos, com processador Intel Core i9 do balacobaco', 7,2 --id do fabricante Dell
);

INSERT INTO produtos(nome, preco, descricao, quantidade, fabricante_id) VALUES(
    'Tablet Android' , 'Tablet com a versão 14 do sistema operacional android, possui tela de 10 polegadas e armazenamento de 128 GB, 64 GB de RAM porque o eliel perguntou.',1500.99, 5,5
);

INSERT INTO produtos(nome, preco, descricao, quantidade, fabricante_id) VALUES(
    'Geladeira' , 'Refrigerador frost-free com acesso á internet', 5000, 12, 6),
    ('IPHONE 18 PRO MAX','CELULAR DA APPLE MUITO SINISTRO', 12666.66, 3, 3),('iPAD MINI','Tablet apple com tela de tv', 4999.01, 5, 3);

INSERT INTO produtos(nome, preco, descricao, quantidade, fabricante_id) VALUES(
    'Xbox series S' , 'Velocidade é desempenho de última geração.', 1997, 5, 8),
    ('Nootbok Motion','Intel Dual Core 4 GB de RAM 128 GB SSD ', 1213.65, 8, 7);
```

---

## Select * FROM produtos;

```sql
SELECT * FROM produtos;

SELECT nome, preco FROM produtos;

SELECT nome, preco,quantidade FROM produto 
WHERE preco < 5000;

-- Mostre nome e descrição somesnte dos produtos da apple

SELECT nome, descricao FROM produtos
WHERE fabricante_id = 3;
```

### Operadores Lógicos: E, OU , NÃO

```SQL
SELECT nome, preco FROM produtos
WHERE preco >= 2000 AND preco <= 6000;

--A QUERY abaixo não retorna registros já que as condições 
SELECT nome, preco FROM produtos
WHERE preco >= 5000 AND preco <= 6000;
```

### OU

```SQL
SELECT nome, preco FROM produtos
WHERE preco > 5000 OR preco <= 3000;

 -- Exiba nome e preço somente dos produtos da apple e Samsung

 SELECT nome, preco FROM produtos
 WHERE fabricante_id = 3 OR fabricante_id = 5;

-- versão usando IN()
SELECT nome, preco FROM produtos
WHERE fabricante_id IN(3,5);

-- versão usando NOT IN()
SELECT nome, preco FROM produtos
WHERE fabricante_id NOT IN(3,5);
```

#### NÃO
```SQL
SELECT nome, descricao, preco FROM produtos
WHERE NOT fabricante_id = 8;

-- versão usandooperador relacional "diferente/diferente"
SELECT nome, descricao, preco FROM produtos
WHERE NOT fabricante_id  != 8;
```