# Servidores

## Como criar um servidor

```
const express = require("express");
const app = express();


app.get(`/`, (req, res) => {
  res.send("Hello World!");
});

app.listen(3000);
```

## Nodemon

- utilitário que monitora as mudanças nos arquivos do seu projeto e reinicia automaticamente o servidor Node. js

- com ele, não precisar ficar reestartando o serviodor


### Instalar o nodemom apenas para desenvolvimento 

No terminal, use -D:

```
npm install -D nodemon
```
### Iniciar um projeto com configurações *default*

Digite no terminal:

```
npm init -y
```

No arquivo package.json altere a seguinte linha:
```
  "scripts": {
    "dev": "nodemon ./index.js"   
  },
```

Executar o script criado no terminal 

```
npm run dev
```

 ##    Insomnia
Substitui o navegador

https://insomnia.rest/download


## Parâmetros de rota

```
app.get(`/home/:exemplo_de_parametro_de_rota`, (req, res) => {
  res.send("Hello $req.params.exemplo_de_parametro_de_rota ");
  req.params
});
```


Quando se digita no navegador < http://localhost/3000/home/XXX >, o parâmetro req possui um objeto que se chama


```
req.params.exemplo_de_parametro_de_rota = XXX
```

## Parâmetros de consulta (Query params)

São parâmetros criados na URL que nós *recuperamos* do servidor. Como se cria uma query param? 

Com a interrogação no endereço do navegador. *?*

< http://localhost:3000/professores?nome=Guido >

O que vier depois da interrogacao é uma query param.

Para criar mais de um parâmetro, utiliza-se o *&*

<http://localhost:3000/professores/?nome=Guido&stack=Backend>

Para recuperar o parâmetro do servidor, usamos:

```
app.get (`./professores`, (req, res)=>{
  req.query;                        //armazena os parametros de consulta
  const {nome, stack} = req.query   // desestrutura os dados
});
```
Nesse exemplo, os parâmetros têm os seguintes valores:

- nome = req.query.nome = Guido
- stack = req.query.stack = Backend


## Controladores

Controladores são funções que controlam o servidor. É a mesma função que usamos no método GET

```
get('./', funcaoControladora)
```

**Se organize!** Coloque todos os controladores em um arquivo ```funcoes.js```, em uma pasta chamada ```./controladores``` ou ```./controllers```.

### Como exportar as funções controladoras que estão escritas em outro arquivo?

No arquivo onde estão as funções escreva:
```
module.exports = {
    funcao1,
    funcao2,
}
```

No arquivo ```index.js``` escreva:

```
const {funcao1, funcao2} = require("./controladores/funcoes.js");
```

## Intermediários (Middlewares)

### Middleware independente

Para criar um intermediario independente usamos o método USE da biblioteca *express* . Nesse exemplo, antes de passar pela ```rota 1```, o intermediario ```app.use``` vai ser verificado.

```
app.use((req,res,next)=> {
   console.log('passei no primeiro intermediario')
   next()
})

app.get( ... rotas 1...)
```
               
 ### Middlewares da rota

Também é possível chamar um intermediario dentro da rota. Nesse caso não usamos o método USE, e sim, uma função que entra como segundo arguento no método GET, antes da função controladora. 

```
const intermediarioDaRota (req, res, next) => {
   // código aqui
   next();
}


app.get('/home', intermediarioDaRota, funcaoControladora)
```
# Passo a passo para criar um servidor

1. Criar arquivos e diretórios
  1.1 ./src/index.js
  1.2 ./src/rotas.js
  1.3 ./src/DB/bancodedados.js
  1.4 ./src/controladores/controlador1.js
  1.5 etc...
2. Instalar express
3. Instalar Nodemon
4. Configurar Nodemon
5. `const express = require("express");`
     
