# Conexão Node.js com PostgreSQL


<img align="center" width="350px" src="https://assets.northflank.com/Group_321_160b91d960.png">



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