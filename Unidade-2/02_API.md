# API
## REST
*Representational state transfer*

- Dados manipulados numa API  REST = recurso 

- conjunto de recursos = coleções

- cada recurso tem um *identificador único e imutável*


## JSON

*JavaScript Object Notation*

- notação para *representar* recursos
- notação para *transitar dados na web*`
- sintaxe igual  JS mas o nome do objeto precisa estar entre aspas

```
{
    "nomeDoObjeto": valorDoObjeto,
}
```
### Métodos / verbos

- GET : listar os recursos ou acessar um recurso específico
- POST: cadastrar recurso na coleção
- PUT: altera um recurso por completo
- PATCH: altera uma parte do recurso na coleção
- DELETE: excluir o recurso da  coleção

```
GET /livros/3  //acessa o recurso 3
```

# Status code

Código | Status geral
 ---| ----
2xx | Sucesso         
4xx | Erro do Cliente 
5xx | Erro do servidor

Código | Status
 ---| ----
200 | OK
201 | Created
204 | No content
400 | Bad request
401 | Unauthorized
403 | Forbidden
404 | Not found
500 | Internal Server Error





