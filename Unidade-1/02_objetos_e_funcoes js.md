# Objetos

Em Java Script, define-se um objeto entre de chaves. Cada popriedade é definida com dois pontos ( `propriedade: valor`) e separadas por vírgula.

```
const pessoa = {
   nome: "José",
   altura: 1.73,
   carro: {
           marca: "Toyota",
          }
};

cont endereco = {
   rua: "Dos Desesperados" 
}

pessoa.nome = "José"

```
> Em Java Script, **arrays são objetos**.

> Se fizermos `obj2 = obj1`, **não** é feita a cópia do primeiro objeto no segundo. Eles ficam apenas *linkados*.


## Desestruturação ou Destructuring 

Para desestruturar objetos: 
```
cont{nome, altura} = pessoa
```

Também é possivel desestruturar arrays: 

```
cont [nome1, nome2] = listaDeNomes;
```

## Spread

O operador spread, representado pelos três pontos (`...`),  é usado para "espalhar" os elementos de um array ou  objeto em outro.


>     spread ... espalhar        

Exemplo 1:
``` 
const objetaoComTudo = {
   ...pessoa
   ...endereco
}
```

Exemplo 2:
```
const arrayOriginal = [1, 2, 3];
const arrayNovo = [...arrayOriginal, 4, 5];
```

Exemplo 3:

```

let array = [0,1,2,3,4];
const [a,b,...resto] = array   

```
No exemplo acima, `a` e `b` recebem os dois primeiros itens do array, e `resto` recebe o resto do array.


# Funções

Definindo uma função da forma tradicional:
```
fuction nomeDaFuncao (parametro1, parametro2) {  
   let resultado;
   return resultado;
}
```

> Os **parâmetros** e o **return** são opcionais.

Definindo uma função no formato *arrow function*:

```
const soma = (x,y) => {
   return x+y;
}
```

> Caso a função seja declarada depois do seu chamamento, a declaração da função e sua implementação são completamente movidas para o topo do escopo, impedindo erros. A isso chamamos de *hoisting*. 

## Métodos

São funções definidas dentro de objetos.

```
cont pessoa = {
   nome: "Jose",
   idade: 30,
   apresentar: funtion () { 
        console.log(`ola ${this.nome}`)   
      },
}

pessoa.apresentar();
```

> `this` é uma palavra reservada para se referir ao próprio objeto.





