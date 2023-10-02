# Programação Assíncrona

> código *síncrono*: para executar a próxima linha, a linha anterior precisa ser finalizada.

> código *assíncrono*: as funções são executadas de forma não linear. Não precisa esperar a execussão da anterior. 

## Event Loop

O Node.js usa event loop, o que permite que o servidor continue a lidar com várias operações de forma assíncrona sem bloquear a execução do programa.

> Um laço de eventos é uma construção de programação que *espera* eventos e mensagens e as despacha num programa de computador. O mecanismo é um laço infinito que é bloqueado até que chegue um evento, que então é tratado. O mecanismo então é reiniciado

<img src="https://cdn.hashnode.com/res/hashnode/image/upload/v1663325652752/J21ZzHc2G.gif" width ="300" >

## Promises

Esse tipo de função tem três status diferentes:

1. Pendente
2. Resolvida
3. Rejeitada

### Exemplo usando a Biblioteca utils-playground

https://www.npmjs.com/package/utils-playground

Para instalar no terminal:
```
npm install utils-playground
```

Para buscar a cidade de um CEP:

```
const {getCityFromZipcode} = require(`utils-playground`);

getCityFromZipcode(`12345678`).than( a => {console.log(`A cidade é $a`);}).catch( erro => {console.log(erro);})
```

Os objetos ```.than()``` e ```.catch()``` tratam as pendências, respectivamente, se for resolvida ou rejeitada.

> `getCityFromZipcode(`12345678`)` é uma promessa.

## Funções ```async``` com  ```await```

Para executar uma função assíncrona apenas depois de outra função assíncrona ter sido executada, é preciso colocá-la dentro do ```.than()``` da primeira função. Mas isso deixa o código pouco legível. Uma alternativa é usar as palavras reservadas ```async``` e  ```await```.


Vamos usar uma função anônima (sem nome), e dizer que ela é assíncrona usando ```async```:
```
async function (){

}
```
Agora vamos uma funções assincrona: 

```
async function (){
    const cidade = getCityFomZipcode(`82174657`);
    console.log(`cidade`);
}();

```

Da forma como está escrito acima, a função ```console.log``` não espera a função ```getCityFromZicode``` terminar de executar, retornando o status pendente. Para esperá-la executar, vamos usar o ```await```.

```
async function (){
    const cidade = await getCityFomZipcode(`82174657`);
    console.log(`cidade`);
}();
```

Para escrever uma função assíncrona usando o padrão *arrow function*, fazemos da seguinte forma.

```
const teste = async () => {}
```

 ## Promise.all()

Essa função resolve várias promessas de uma única vez. Ela mesma é uma função assíncrona, por isso, podemos usar o `await` apenas nela. 

```
app.get(`/`, async(req, res) => {
    const  cidade1 = getCityFromZipcode(`12345678`)
    const  cidade2 = getCityFromZipcode(`87654321`)

    const promessa = await Promise.all([cidade1, cidade2])
})
```

Nesse exemplo, agora a variável `promessa` contém um array com os resultados da busca de `cidade1` e `cidade2`.





