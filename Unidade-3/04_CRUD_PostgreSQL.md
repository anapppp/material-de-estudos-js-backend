# CRUD em PostgreSQL
![](https://pbs.twimg.com/tweet_video_thumb/C81toHkXgAAZ7lB.jpg)

> C = Create

> R = Read

> U = Update

> D = Delete


## Exemplo: criando tabela produtos

```
create database aula_crud;
```

```
create table if not exists produtos (
	id serial primary key,
  	nome text,
  	descricao text,
  	preco integer,
  	categoria text
);
```

```
insert into produtos (nome, descricao, preco, categoria) values ('Caderno', 'Linda Camisa', 5990, 'Roupas');
```

```
insert into produtos (nome, preco, categoria) values ('Caderno', 2000, 'Material escolar');
```

```
insert into produtos (nome, descricao, preco, categoria) values ('Calça Jeans', NULL, 12900, 'Roupas'),('Bermuda', 'Bermuda longa preta', 12900, 'Roupas');
```

```
update produtos set nome = 'Caderno de 10 materias' where id = 3;
```

```
update produtos set categoria = 'Calças', preco = 12950 where descricao is null;
```

```
update produtos set nome = 'Caderno'; 
```
> ⚠️ **NUNCA FAÇA UPDATE SEM WHERE**

```
delete from produtos where id = 1;
```

```
delete from produtos where descricao is null;
```

```
delete from produtos; 
```
> ⚠️ **NUNCA DELETE SEM WHERE**

```
select * from produtos;
```

