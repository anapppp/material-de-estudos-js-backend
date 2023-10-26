# Consultas em PostgreSQL

## Paginação - mostrando páginas 1, 2, 3, etc...
```sql
select * from musicas offset 0 limit 10 -- pag 1
select * from musicas offset 10 limit 10 -- pag 2
select * from musicas offset 20 limit 10 -- pag 3
```

## Ordenando os resultados
```sql
select * from musicas where compositor = 'Schubert' order by id desc 
```
```sql
select * from musicas where compositor = 'Schubert' order by composicao asc
```
> **Coringa:** O símbolo `%` selecioana qualquer quantidadede caracteres até a sua posição

```sql
select * from musicas where composicao like 'Violin%'
```
```sql
select * from musicas where composicao like '%Sonata%'  -- case sensitive
```
```sql
select * from musicas where composicao ilike '%piano%'  -- nao eh case sensitive
```
```sql
select * from musicas where tempo > 2*60 limit 10
```
```sql
select * from musicas order by id limit 20
```

## Join
![join](https://www.csestack.org/wp-content/uploads/2020/10/sql-table-joins.png)

### Inner Join

Retornando todos os registros da tabela *empresas*  e *filiais* cujo *id*s sejam iguais.

```sql
select * from empresas join filiais on empresas.id = filiais.empresas.id;
```
> Tanto faz escrever `inner join` ou `join`

Forma mais compacta de escrever chamando empresas de *e* e filiais de *f*.
```sql
select e.id as empresaID, f.i as filialID, e.nome, f.pais 
from empresas e join filiais f on e.id = f.empresas.id;
```

```sql
select e.id as empresaID, f.i as filialID, e.nome, f.pais, p.nome as funcionario 
from empresas e join filiais f on e.id = f.empresas.i 
join pessoas p on p.empresa_id = e.id;
```

### Left Join e Right Join
Left join: retorna *todas as colunas da tabela a esquerda* e tenta juntar com a tabela da direita da query. Os registros da tabela da esquerda que não tiverem correspondentes com a da direita também são retornados, mas como `NULL`.

Right join: a mesma coisa, mas com relacão a tabela da direita

```sql
select e.if as empresasId, f.id as filiaisId, e.nome, f.pais from empresas e left join filiais f on e.id = f.empresa_id;
```

### Full Join

Retorna *todas as colunas das tabelas da esquerda e da direita* e tenta juntar. Os registros que não tiverem correspondentes são retornados como `NULL`.
```sql
select e.if as empresasId, f.id as filiaisId, e.nome, f.pais from empresas e left join filiais f on e.id = f.empresa_id;
```

> `full join` é o contrário de `inner join`.
