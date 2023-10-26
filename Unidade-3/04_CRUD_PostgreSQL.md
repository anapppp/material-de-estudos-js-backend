# CRUD em PostgreSQL
<img src="https://pbs.twimg.com/tweet_video_thumb/C81toHkXgAAZ7lB.jpg" width = "300" />



> C = Create

> R = Read

> U = Update

> D = Delete


## Exemplo: criando tabela produtos

```sql
create database aula_crud;
```

```sql
create table if not exists produtos (
	id serial primary key,
  	nome text,
  	descricao text,
  	preco integer,
  	categoria text
);
```

```sql
insert into produtos (nome, descricao, preco, categoria) values ('Caderno', 'Linda Camisa', 5990, 'Roupas');
```

```sql
insert into produtos (nome, preco, categoria) values ('Caderno', 2000, 'Material escolar');
```

```sql
insert into produtos (nome, descricao, preco, categoria) values ('Calça Jeans', NULL, 12900, 'Roupas'),('Bermuda', 'Bermuda longa preta', 12900, 'Roupas');
```

```sql
update produtos set nome = 'Caderno de 10 materias' where id = 3;
```

```sql
update produtos set categoria = 'Calças', preco = 12950 where descricao is null;
```

```sql
update produtos set nome = 'Caderno'; 
```
> ⚠️ **NUNCA FAÇA UPDATE SEM WHERE**

```sql
delete from produtos where id = 1;
```

```sql
delete from produtos where descricao is null;
```

```sql
delete from produtos; 
```
> ⚠️ **NUNCA DELETE SEM WHERE**

```sql
select * from produtos;
```

