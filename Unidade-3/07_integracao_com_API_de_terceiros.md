# Integração com API de terceiros

Para fazer integração com outras APIs, precisamos enviar requisições HTTP. Para isso, vamos usar a biblioteca `axios`.

## Biblioteca `axios`

Documentação [aqui](https://axios-http.com/ptbr/docs/intro)
```
npm install axios
```

> `axios`` é baseado em promessas

## Recebendo informações de outra API

Nesse exemplo, tenho uma API rodando na porta 3000 e estou buscando os dados retornados da porta 3001 na URL http://localhost:3001/carros. 

> aqui se usa o verbo **GET**

```
const express = require('express')
const app = express()
const axios = require('axios')

app.use(express.json())
app.get('/', async (req, res) => {
    const resultadoAxios = await axios.get('http://localhost:3001/carros')
    res.json(resultadoAxios.data)
})
app.listen(3000)
```

## Enviando informações para outra API

Nesse exemplo, tenho uma API rodando na porta 3000 e estou cadastrando na API2, que roda na porta 3001, um novo objeto. 

> aqui se usa o verbo **POST**

```
const express = require('express')
const app = express()
const axios = require('axios')

app.use(express.json())
app.get('/', async (req, res) => {

    const novoCarro = {
        marca: "Fusca",
        ano: "1969"
    }
    const resultadoAxios = await axios.post('http://localhost:3001/carros', novoCarro)
    res.json(resultadoAxios.data)
})
app.listen(3000)
```

A  URL http://localhost:3001/carros da API2 também usa o verbo POST, para icluir mais um carro no banco de dados. É como se a API1 funcionasse como a requisição no body que fazemos através do Insomnia.

## Criando uma instância usando axios 

Podemos usar o `axios.create`  para criar uma instancia com todas as configurações, para reutilizá-la varias vezes na funcao armazenada.


```
// CRIANDO UMA INSTANCIA
const instanciaAxios = axios.create({
    baseURL: "http://localhost:3001"    // domínio base da API que você quer se comunicar 
})

// USANDO A INSTANCIA
app.get('/', async (req, res) => {
    const novoCarro = {
        marca: "Fusca",
        ano: "1969"
    }
    const resultadoAxios = await instancioAxios.post('/carros', novoCarro)
    res.json(resultadoAxios.data)
})
```

> [Aqui](https://axios-http.com/ptbr/docs/req_config) você pode obter todas as configurações opcionais para fazer uma requisição.

## Gateway de pagamento

Vamos usar o [Stripe](https://stripe.com/br)