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

INSERT INTO fabricante(nome) VALUES('LG'), VALUES('SAMSUNG'), VALUES('BRASTEMP'); 

INSERT INTO fabricante(nome) VALUES('POSITIVO'), VALUES('MICROSOFT');

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
```