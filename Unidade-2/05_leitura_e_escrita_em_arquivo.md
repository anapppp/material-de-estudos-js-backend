# Leitura e Escrita de Arquivos

## Leitura de arquivos

Usamos a biblioteca nativa do Java Script *File System*.
 - as funções são assíncronas 
 - utilizam funções callback

Para importar a biblioteca:
 ```javascript
 const fs = require(`fs`);
 ```

 Leitura de arquivo sincrono:

 ```javascript
 const a = fs.readFileSync(`a.txt`).tostring();
 ```

 Leitura assíncrona
 ```javascript
 fs.readFile(`a.txt`, (erro, data)=> {
    if(erro){
        //faca alguma coisa
    }else {
        console.log(data.toString())
    }
 })
 ```

 ## Requisições assíncronas com promisses

 ```javascript
 const fs = require(`fs/promises`)
 ```

 ### Lendo arquivos JSON

Utiliza-se o comando `JSON.parse()`

 ```javascript
 const fs = require(`fs/promises`)

 (async function () {
    const arquivoJson = await fs.readFile(`tete.json`);
    const pessoas = JSON.parse(arquivoJson);
    })();
 ```

## Escrita de arquivos

```javascript
fs.writeFile(''./src/a.txt, 'Olá')
```
> Atenção: Essa comando sobrescreve o arquivo caso ele já exista.

### Escrevendo arquivos em JSON

```javascript
const pessoasStringfy = JASON.stringfy(pessoas);
await fs.writeFile(`./src/usuarios.json`, pessoasStringfy)
```
