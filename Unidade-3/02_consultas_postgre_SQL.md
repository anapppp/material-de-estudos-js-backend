# Consultas em PostgreSQL

## Paginação - mostrando páginas 1, 2, 3, etc...
```
select * from musicas offset 0 limit 10 -- pag 1
select * from musicas offset 10 limit 10 -- pag 2
select * from musicas offset 20 limit 10 -- pag 3
```

## Ordenando os resultados
```
select * from musicas where compositor = 'Schubert' order by id desc 
```
```
select * from musicas where compositor = 'Schubert' order by composicao asc
```
> **Coringa:** O símbolo `%` selecioana qualquer quantidadede caracteres até a sua posição

```
select * from musicas where composicao like 'Violin%'
```
```
select * from musicas where composicao like '%Sonata%'  -- case sensitive
```
```
select * from musicas where composicao ilike '%piano%'  -- nao eh case sensitive
```
```
select * from musicas where tempo > 2*60 limit 10
```
```
select * from musicas order by id limit 20
```