# Conexão Node.js com PostgreSQL
![Group_321_160b91d960](https://github.com/anapppp/material-de-estudos-js-backend/assets/70073296/d6a5bdeb-0d4f-4194-b846-380675ea5c97)

## Biblioteca `node-postgres`

> Acesse a documentação [aqui](https://node-postgres.com/).

Instalando

```
npm install pg
```

## Conexão simples com o banco de dados usando `Client()`

```
const express = require('express');
const app = express();
const { Client } = require('pg');
app.use(express.json());

app.get('/', async (req, res) => {
    const client = new Client({
        host: 'localhost',
        port: '5432',
        user: 'postgres',
        password: '123456',
        database: 'aula_conexao_node_pg'
    });
    try {
        await client.connect();
        const resultado = await client.query('select * from empresas')    // AQUI SE EXECUTA A QUERY SQL
        await client.end();
        return res.json(resultado.rows);
    } catch (error) {
        console.log(error.message);
    };
});

app.listen(3000);
```


## Conxão com o banco de dados usanto `Pool()`

```
const express = require('express');
const app = express();
const { Pool } = require('pg');
app.use(express.json());

const pool = new Pool({
    host: 'localhost',
    port: '5432',
    user: 'postgres',
    password: '123456',
    database: 'aula_conexao_node_pg'
});

app.get('/', async (req, res) => {
    try {
        const resultado = await pool.query('select * from empresas')    // aqui se executa uma query no SQL
        return res.json(resultado.rows);
    } catch (error) {
        console.log(error.message);
    };
});

app.listen(3000);
```

> Nas nossas aplicações *sempre* vamos  usar o `Pool()` por ser muito mais performático.

> Vamos colocar todos os pools em um arquivo separado chamado `conexao.js`

## Como passar valores dinâmicos na query

> ⚠️ SQL Injection
>> Se fizermos 
>> ```
>> const resultado = await pool.query(`select * from empresas where id=${id}`)
>>```
>> estamos sujeitos a um ataque hacdddker chamado **SQL Injection**. Basta passar na URL `http://localhost:3000/16 or 1=1` que todo o banco de dados 'e retornado.
>> Por isso **NUNCA** fa'ca concatenacão dentro da string de requisição da query. 

Para evitar ataques SQL Injection, faça dessa forma:

```
app.get('/:id', async (req, res) => {
    const { id } = req.params
    try {
        // const resultado = await pool.query(`select * from empresas where id=${id}`)  // NAO FACA ISSO
        const query = `select * from empresas where id=$1`;
        const params = [id];
        const resultado = await pool.query(query, params)
        return res.json(resultado.rows);
    } catch (error) {
        console.log(error.message);
    };
});
```

## Paginação de resultados

```
const express = require('express');
const app = express();
app.use(express.json());
const pool = require(`./conexao`)


app.get('/', async (req, res) => {
    const { pagina, porPagina } = req.query;
    try {
        const query = `select * from pessoas order by id asc limit $1 offset $2`;
        const offset = pagina === 1 ? 0 : (pagina - 1) * porPagina;  // Se a pag == 1, offset =0; senao, offset=(pag-1)*porPagina
        const params = [porPagina, offset];
        const resultado = await pool.query(query, params);
        const resultPrint = {
            pagina,
            porPagina,
            numeroDeRegistros: resultado.rowCount,
            registros: resultado.rows
        }
        return res.json(resultPrint);
    } catch (error) {
        console.log(error.message);
    };
});

app.listen(3000);
```

