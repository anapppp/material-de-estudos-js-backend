# Comanos básicos em Java Script

> *Para saber mais:* O [MDN Web Docs](https://developer.mozilla.org/pt-BR/) é uma ampla plataforma com documentação para desenvolvedores web, incluindo tecnologias como *HTML*, *CSS*, *JavaScript* e *APIs*. 

## Declaração de variável

- `const`        declara variável constante, inclusive texto
- `let`          declara variável cujo valor pode ser alterado

> Use o padrão **camelCase** : Comece o nome das variáveis com letra minúscula                                      

## String template

É uma forma de criar strings que permite a incorporação de expressões e variáveis diretamente dentro da string. É definida entre *crases* 

```
let idade = 35;
console.log('Minha idade é ${idade}');
```

>  `variavel.toFixed(2)` imprime variável com duas casas decimais


## Escopo
É a estrutura limtada entre chaves. 
```
 { 
   ...escopo... 
 }
```
> variáveis criadas fora do escopo valem dentro do escopo também, o contrário não é verdadeiro.

> váriaveis criadas no escopo (entre chaves) são "apagadas" depois das chaves

## Operadores

Operador    | Resultado 
---------   | --------- 
`x += 3`    | x = x+3
`x -= 3`    | x = x-3
`x *= 3`    | x = x*3
`x /= 3`    | x = x/3
`x = a % b` | resto da divisao de 12 por 5 (*se `a` e `b` forem inteiros, o operador `%` **sempre** retorna um inteiro*)
`x++`       | x = x+1 (*primeiro retorna depois incrementa*) 
`x--`       | x = x-1 (*primeiro retorna depois incrementa*)
`++x`       | x = x+1 (*primeiro incrementa depois retorna*) 
`--x`       | x = x-1 (*primeiro incrementa depois retorna*)  

### Biblioteca Math

Biblioteca de matemática nativa.

Raiz quadrada: 
```
y = Math.sqrt (9);
``` 
Potência:
```
y = Math.pow (2,3);
```

## Condicionais


Operador   | Resultado
---------- | ----------
`==`       | operador "é igual" ( *3=="3" retorna true* )
`===`      | operador "é idêntico" ( *retorna true se o valor **e** o tipo forem iguais*)
`!=`       | é diferente
`!==`      | não é idêntico  
`&&`       | comparador E
`\|\|`       | comparador OU
`!`        | negação




### Comando `if`

```
if{
   } else if{
      }else{
}
```

Se a condiçãoo tiver só uma linha, não precisa usar chaves

```
if
   condicao 1
else
   condicao 2
```

Para condicionar o valor armazenado em uma variável, usa-se o *ternário*

```
const variavel = ( x === cond1 ? valorCondTrue : valorCondFalse ) 
```

## Arrays

É possivel adicioinar elementos de diferentestipos em um array.

```
cont varArray = [1,2,3.3, "quatro"];
```

O tamanho de um array é dado pela propriedade `length`

```
tamanhoDoArray = varArray.length
```

O índice de um array começa em **0** e o último é **tamanhoDoArray -1**


Comando                 | Descrição
----------------------- | --------------------------------------
varArray.push("aaa")    | adiciona um valor no final do array
varArray.pop()          | remove o ultimo item da lista
varArray.unshift("bbb") | adiciona um valor no inicio do array
varArray.shift()        | remove o primeiro item da lista


## Loops

Opção 1: 
```
let i=0;
  while( i<5 ){
   console.log(array[i]);
   i++;
}
```

Opção 2:
 ```
for (let i=0; i<5; i++){
   console.log(array[i]);
}
```

Opção 3:

```
for (let item of varArray){
   console.log("item");
}
```
	


