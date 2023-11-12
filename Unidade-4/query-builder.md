# Query Builder

Vamos usar a biblioteca [knex](https://knexjs.org/guide/query-builder.html#identifier-syntax)

Primeiramente devemos montar um arquivo chamado 'conexao.js'

```javascript
const knex = require('knex')({
    client: 'pg',
    connection: {
        host: 'localhost',
        user: 'postgres',
        password: '123456',
        database: 'dindin'
    }
})

module.exports = knex
```

Projeto básico usando knex

```javascript
const express = require('express')
const knex = require('./conexao.js')
const app = express()

app.use(express.json())

app.get('/', async (req, res) => {
    const categorias = await knex('categorias')
    return res.json(categorias)
})

app.listen(3000)
```

## Comandos úteis

Imprime no terminal o debug da query:
```javascript
    const categorias = await knex('categorias').debug()
```

Possibilita escrever os comandos SQL diretamente:
```javascript
    const categorias = await knex.raw('select * from "categorias"')
```

## Fazendo consultas

```javascript
    const categorias = await knex('categorias').where('id', 1)
```

```javascript
    const categorias = await knex('categorias').where('id', '!=', 1)
```

```javascript
    const categorias = await knex('categorias').where({ descricao: 'Alimentação' })
```

Retorna o primeiro registro:
```javascript
    const categorias = await knex('categorias').first()
```

Seleciona as colunas que serão retornadas:
```javascript
    const categorias = await knex('categorias').select('id','categoria')
```

Mostra apenas os parâmetros únicos:
```javascript
    const categorias = await knex('categorias').distinct('nome', 'email')
```
Agrupa e conta:
```javascript
    const categorias = await knex('categorias').select('email').groupBy('email').count()
```

Limit e offset
```javascript
    const categorias = await knex('categorias').limit(5).offset(2)
```

## Inserindo registro no banco de dados

Insere e retorna o ID.

```javascript
const ana = {
    nome: 'Ana',
    email: 'anapaula@gmail.com'
}

const joao = {
    nome: 'joao',
    email: 'joao@gmail.com'
}
    const  agenda = await knex('usuarios').insert([ana, joao]).returning('id')
```

## Join

```javascript
    const anotacoes = await knex('anotacoes').join('agenda', 'anotacoes.agenda_id').select('anotacoes_*')
```