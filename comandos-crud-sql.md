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

### UPDATE

```SQL
UPDATE produtos SET preco = 6549.74
WHERE id =4;

-- Altere a quantidade dos produtos da apple e da sansung para 20

UPDATE produtos SET quantidade = 20
WHERE fabricante_id = 3 OR fabricante_id =5;
```

---
## DELETE

```SQL
DELETE FROM fabricante WHERE id=1;
DELETE FROM fabricante WHERE id=4;
```

## SELECT: outras formas de uso

### Cassificando
```SQL
SELECT nome, preco FROM ORDER BY nome;
SELECT nome, preco FROM ORDER BY preco;
SELECT nome, preco FROM ORDER BY preco DESC;

-- DESC: CLASSIFICAÇÃO EM ORDEM DECRECENTE
-- ASC: CRECENTE

SELECT nome, preco FROM produtos 
WHERE quantidade = 20 ORDER BY nome;
```

### BUSCA DE DADOS 
```SQL
SELECT nome, descricao FROM produtos
WHERE descricao  LIKE '%tela%' OR nome LIKE '%tela%';

-- BUSCA em palavra indicada a qualquer posição no texto
```

### Operações e funções de agregação

```SQL
SELECT SUM(preco) as Total  FROM produtos;

SELECT nome as Produto, preco as "Preço" FROM produtos;
SELECT nome Produto, preco "Preço" FROM produtos;

-- MÉDIA
SELECT AVG(preco) as "Média dos Preços" FROM produtos; 
SELECT ROUND(AVG(preco), 2) as "Média dos Preços" FROM produtos; 

-- CONTAGEM 
SELECT COUNT(id) as "Qtd de Produtos" FROM produtos;
SELECT COUNT(DISTINCT fabricante_id) as "Qtd de Fabricantes com Produtos" FROM produtos;

-- distinct É UMA CLÁUSULA/FLAG que evita a duplicidade na contagem de registros
```


### Oprações matemáticas

```SQL
SELECT  nome, preco, quantidade, (preco * quantidade) as Total FROM produtos;
```

### Segmentação/Agrupamento de resultados
```SQL
SELECT fabricante_id, SUM(preco) FROM produtos GROUP BY fabricante_id;
```

---

## Consultas (Queries) em duas ou mais tabelas relacionadas(JUNÇÃO/JOIN)

```SQL
-- SELECT tabela.coluna, tebela.coluna
SELECT produtos.nome, fabricante.nome
-- INNER JOIN é o comando que permite JUNTAR as tabelas
FROM  produtos INNER JOIN fabricante
-- ON comando para indicar a forma/critério da junção
ON produtos.fabricante_id = fabricante.id;
-- chave estrangeira        chave primaria



SELECT produtos.nome as produto, fabricante.nome as fabricante
FROM  produtos INNER JOIN fabricante
ON produtos.fabricante_id = fabricante.id;
```

### Nome do produto, nome do fabricante, ordenados pelo nome do produto

```SQL
SELECT
    produtos.nome as produto,
    produtos.preco as "Preço",
    fabricante.nome as fabricante
FROM produtos INNER JOIN fabricante
ON produtos.fabricante_id = fabricante.id
ORDER BY produtos DESC; -- ou produtos.nome
```

### Fabricante, soma dos preços e quantidade de produtos

```SQL
SELECT
    fabricante.nome AS fabricante,
    SUM(produtos.preco) AS Total,
    COUNT(produtos.fabricante_id) AS "QTD de produtos"
FROM produtos INNER JOIN fabricante
ON produtos.fabricante_id = fabricante.id
GROUP BY fabricante;
ORDER BY total;
```

### Desafio 1: Trazer a quantidade de produtos de cada fabricante e a soma da quantidade/estoque destes produtos

```SQL
SELECT 
    fabricante.nome AS fabricante, 
      SUM(produtos.quantidade) AS "QTD de estoque",
COUNT(produtos.id) AS "QTD de produtos"
    FROM produtos INNER JOIN fabricante
ON produtos.fabricante_id = fabricante.id
GROUP BY fabricante;
```

### Desafio 2: Trazer a quantidade de produtos de cada fabricante e a soma da quantidade/estoque destes produtos, SOMENTE dos fabricantes que NÃO POSSUEM produtos

```SQL
SELECT 
    fabricante.nome AS fabricante, 
      SUM(produtos.quantidade) AS "QTD de estoque",
COUNT(produtos.id) AS "QTD de produtos"
    FROM produtos RIGHT JOIN fabricante
ON produtos.fabricante_id = fabricante.id
GROUP BY fabricante;
```