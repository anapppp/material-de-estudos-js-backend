# Deploy

## Variável de ambiente


Variáveis sensíveis são armazenadas em um arquivo `.ENV`. Vamos usar a variável `process.env`, que retorna as informações do sistema operacional. 

No arquivo `.ENV`

```
PORT=3000
```

Por padrão o arquivo `.ENV` precisa estar junto ao `packge.jason`. No `intex.js` fazemos:

```javascript
require(`dotenv`).config()

port = process.env.PORT || 3000
app.get.listen(port)
```
Se o arquivo `.ENV` estiver na pasta `./src` é preciso especificar a pasta:

```javascript
require(`dotenv`).config({
        path: './src/.env',
    })
```

## Biblioteca CORS

Estabelece permissão de domínios que podem acessar a API.

```
npm install cors
```

No arquivo `index.js`:

```javascript
const express = require(`express`)
const cors = require(`cors`) 

const app = express()

app.use(cors({
    origin:['site1.com.br', 'site2.com.br']
}))  // opcao para estabelecer dominios permitidos

app.use(cors()) //opcao para permitir qualquer dominio

// A partir daqui, colocar todas as suas rotas

```