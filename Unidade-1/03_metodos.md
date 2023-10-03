## Métodos

São funções definidas dentro de objetos.

```
cont pessoa = {
   nome: "Jose",
   idade: 30,
   apresentar: funtion () { 
        console.log(`ola ${ this.nome } `)   
      },
}

pessoa.apresentar();
```

> `this` é uma palavra reservada para se referir ao próprio objeto.

## Métodos de string

```
frase = " Eu estou aprendendo a programar na Cubos Academy";

console.log(frase.includes("Cubos", 3));  //procura a string dentro da string a partir do indice 3
console.log(frase.indexOf("e", 10));  //retorna o indice se encontra o caracter
console.log(frase.lastIndexOf("")) //reotrna o indice  onde esta um caracter lendo de tras pra frente
console.log(frase.slice(-10)) //corta a string, se o argumento for negativo, coonta de tras pra frente
console.log(frase.split(" ")) //fatia a string toda vez que o caractere " " aparecer, retorna um array 
console.log(frase.replace("Eu estou", "A Ana está")) // busca e substitui
console.log(frase.toUpperCase()) //retorna a string toda em maiuscola
console.log(frase.trim())  // REMOVE ESPACOS NO INICIO E NO FIM DA STRING
console.log(frase.padStart(50, "0000***")) // Insere o caractere "*" ate a strig ter 50  caracteres
console.log(String(10.05)) //transforma o numero em string
```

## Métodos de Arrays

```
array = ['a', 'b', 'c', 'd', 'e'];

objeto = [{
    id: 5,
    parametro: "b",
},
{
    id=  3,
    parametro = "b"
}];


array.length() //retorna o tamanho
array.push()   //insere no fim
array.pop()    //remove do fim
array.unshift() //insere no inicio
array.shift()   //remove do inicio

array.indexOf(a)   //retorna o index da primeira ocorrencia de a
array.includes(a)  // retorna true ou false se a está no array
array.reverse()   // reverte a ordem dos itens do array
array.join("_") //junta todos os itens do array em uma string seprado por "_". Se nao passar nada, separa por ","
array.concat(a)  //concatena a no array
array.slice(1, 3)  //fatia entre os indices 1 e 3, 1 incluso, 3 excluso
array.splice(a, b, c)   //a = a partir de onde vc quer mudar o array, b = qtos vc quer deletar, se nao colocar nada apaga tdo depois de a. RETORNA os itens removidos E MODIFICA o array modificado. c elementos pra adicionar a lista

```

## Funções Callbacks

```
const interval = setInterval(fundcao, 2000) ///executa a funaco a cada 2s
clearInterval(interval)  //para o setInterval
setTimeout(funcao, 5000) // executa a funcao apos 5s
array.every(funcaoteste)  // retorna true ou false se todos os  itens de um array passarem pelo teste
array.some(funcaoteste)   // retorna true ou false se apenas um elemento passar no teste
array.find(funcaoteste)   // retorn o primeiro elemento do array que passar no teste
array.findIndex(funcaoteste)  //retorna o indice do primeiro elemento que pssar na funcao teste
array.filter(funcaoteste) //retorna um array com todos os elementos que passem na funcao teste
array.map(funcao) //retorna um novo array com o que retorna na funco para cada elemento do array

```

### Método `.sort()` 

Se colocar um argumento positivo, a funcao inverte a ordem.Se entrar um argumento negativo, ele ordena a depois b

```

array.sort()  // ordena ela tabela UNICODE. Pode receber uma funcao callback
array.sort((a, b) => a - b);   //ordena numeros em ordem crescente 
array.sort((a, b) => b - a);   //ordena numeros em ordem decrescente
objeto.sort((a - b) => a.id - b.id); //ordena um objeto pelo id 
array.sort((a, b) => a.localeCompare(b));  // ordena strings em ordem alfabetica
array.sort((a, b) => b.localeCompare(a));  // ordena strings em ordem alfabetica decrescente
```

### Método `.reduce()`

```
array.reduce((acumulador, valorAtual, índiceAtual, array) => LOGICA DE REDUCAO)

array.reduce((acc, currentValue) => acc + currentValue, 0);  //soma todos os itens de um array
array.reduce((maxValue, currentValue) => Math.max(maxValue, currentValue), -Infinity); // encontra o valor maximo
array.reduce((minValue, currentValue) => Math.min(minValue, currentValue), Infinity); //encontra o valor minimo
array.reduce((maior, atual) => Math.max(maior, atual));  // Utilizando o método reduce para encontrar o maior valor

array.reduce((a, b) => a + b, 0);  //soma todos os itens de um array
array.reduce((a, b) => Math.max(a, b), -Infinity); // encontra o valor maximo
array.reduce((a, b) => Math.min(a, b), Infinity); //encontra o valor minimo
array.reduce((a, b) => Math.max(a, b));  // Utilizando o método reduce para encontrar o maior valor 

```

