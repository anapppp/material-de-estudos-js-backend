# Funções em PostgreSQL

## Funções gerais

- conta o número de registros
```sql
select count(*) from usuarios where idade >= 18;   
```
```sql
select count(*) as "numeroUsuarios" from usuarios where idade >= 18;  
```

- concatenar
```sql
select nome || ' - ' ||  email as "nome - email"from usuarios; 
```
```sql
select concat(nome, ' - ', email, ' (', idade, ')') as "nome - email (idade)" from usuarios; 
```

- calcula a média
```sql
select avg(idade) as "mediaIdade" from usuarios; 
```
- arredonda para uma casa decimal 
```sql
select round(avg(idade),1) as "mediaIdade" from usuarios;  
```
- seleciona a menor idade registrada
```sql
select min(idade) from usuarios; 
```
- retona a maior data
```sql
select max(cadastro) from usuarios;  
```
- soma todas as idades menores que 18
```sql
select sum(idade) from usuarios where idade <18;  
```
- converte o campo idade para texto
```sql
select idade::text from usuarios;
```
- converte formato, mas nao altera o nome  coluna
```sql
select cast (idade as text) from usuarios; 
```

## Funções de tempo e data
- retorna o momento atual
```sql
select now(); 
```
- retorna todas as datas posteriores a agora
```sql
select * from usuarios where cast(cadastro as date) > now(); 
```
- retorna todas as datas posteriores a agora
```sql
select * from usuarios where cast(cadastro as timestamp) > now(); 
```
- retorna apenas a data
```sql
select cast(cadastro as date) from usuarios; 
```
- retorna apenas a hora
```sql
select cast(cadastro as time) from usuarios; 
```
- retorna data e hora
```sql
select cast(cadastro as timestamp) from usuarios; 
```
- compara datas e retorna a diferenca
```sql
select age('2022-03-16 12:00:00', '2023-05-16 12:03:00'); 
```
- compara com o momento atual
```sql
select age(cast('2022-03-16 12:00:00' as timestamp)); 
```
## Outros exemplos

```sql
select *,age(cast(cadastro as timestamp)) from usuarios where cast(cadastro as timestamp) < now();
```
> `coalesce` : Se o campo for (NULL) substitui pelo proximo campo
```sql
select concat(nome, ' - ', coalesce (telefone, 'telefone nao preenchido')) from usuarios; 
```
- retorna quantos individus de cada idade tem no banco
```sql
select nome from usuarios group by *'ana'; -
```
- retorna quantos individus de cada idade tem no banco
```sql
select idade, count(id) from usuarios group by idade;
```         
