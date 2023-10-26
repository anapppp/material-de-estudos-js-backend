# Datas em Java Scrip

O Java Script tem o seguinte objeto para armazenar e manipular datas:

```javascript
const momentoAtual = new Date()
```
Este comando retorna o **momento** atual no formato ISO no **horário de Greenwich**.

Para obter outras datas, utiliza-se o seguinte formato 

```javascript
const ano = 2023, mes = 0, dia = 1;


const data = new Date (ano, mes, dia, hora, minuto, segundos, milisegundos)
```

Nesse exemplo é contablizado o momento atual no fuso 0 graus relativo ao fuso que esta configurado na sua máquina. 

> A contagem dos meses começa em *ZERO*
>> Janeiro = 0; Fevereiro = 1

> Já os dias do mês começam em 1 🫠


## Timestamp

É um número que representa a quantidade de milisegundos desde 1 de janeiro de 1970 à 00:00:00.000 em Greenwich.

> Para obter o timestamp coloque um `+` antes da data, ou usando o `.getTime()`.

```javascript
const data = new Date(2023, 0, 1)

console.log(+data);
console.log(data.getTime());
```

Para converter um timestamp em data, use apenas um argumento em `new Date()`:

```javascript
const data = new Date(dataEmTimestamp);
console.log(data);
```

Para comparar datas, use *sempre* o timestamp.

```javascript
+(new Date(0)) === + (new Date());
```


>> `(new Date(0)) === (new Date())` retornaria `false` pois dessa forma se está comparando os lugares de armazenamento na memória.

## Geters e Setters

`const agora = new Date()`

- `agora.getDay()` retorna o dia da semana
- `agora.getMonth()` retorna o mês
- `agora.setDate(4)` muda o dia para 4

## Formatando Datas

- `agora.toLocaleString()`: formata para o horario local

- `agora.toLocaleString("en-US")`: formata para o formato dos EUA.

Existem muitas outras opções de formatação.


## Bibioteca date-fns

https://date-fns.org/


## `.toISOString()`

O método `toISOString()` retorna uma cadeia de caracteres (string) simplificada no formato ISO extendido (ISO 8601), que é sempre 24 ou 27 caracteres de tamanho (`YYYY-MM-DDTHH:mm:ss.sssZ` ou  `±YYYYYY-MM-DDTHH:mm:ss.sssZ`, respectivamente).
