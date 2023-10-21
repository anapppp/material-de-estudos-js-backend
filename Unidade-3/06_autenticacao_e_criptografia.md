# Autenticação e Criptografia

Vamos usar a biblioteca `bcrypt`. Documentação [aqui](https://www.npmjs.com/package/bcrypt).

```
npm install bcrypt
```
## Criar e checar senhas com promisses

Documentação [aqui](https://www.npmjs.com/package/bcrypt#with-promises).

Criar senha:
```
bcrypt.hash(myPlaintextPassword, saltRounds).then(function(hash) {
    // Store hash in your password DB.
});
```
O parâmetro `saltRounds` está relacionao com o custo de processamento para criar a criptografia. O valor recomendad é *10*. Não se recomenda passar desse valor.

Checar senha:

```
// Load hash from your password DB.
bcrypt.compare(myPlaintextPassword, hash).then(function(result) {
    // result == true
});
bcrypt.compare(someOtherPlaintextPassword, hash).then(function(result) {
    // result == false
});
```

##  Cadastro de usuário usando criptografia

```
const cadastrarUsuario = async (req, res) => {
    const { nome, email, senha } = req.body

    try {
        const senhaCriptografada = await bcrypt.hash(senha, 10)
        const { rows } = await pool.query(
            'insert into usuarios (nome, email, senha) values ($1, $2, $3) returning *',
            [nome, email, senhaCriptografada]
        )

        return res.status(201).json(rows[0])
    } catch (error) {
        return res.status(500).json('Erro interno do servidor')
    }
}
```

## Login de usuário usando criptografia

Para login usa-se o verbo `POST`.

``` 
rotas.post('/login', login)
```

Checando usuário e senha:
```
const login = async (req, res) => {
    const { email, senha } = req.body
    try {
        // checando se o usuário se encontra no banco de dados
        const usuario = await pool.query(`select * from usuarios where email = $1`, [email])
        if (usuario.rowCount < 1) {
            return res.status(404).json({ mensagem: 'E-mail ou senha inválidos.' })
        }
        // checando a senha
        const senhaValida = await bcrypt.compare(senha, usuario.rows[0].senha)  // compara a senha informada pelo usuario com  hash que está armazenada no banco de dados
        if (!senhaValida) {
            return res.status(400).json({ mensagem: "E-mail ou senha inválidos." })
        }
        return res.json('Usuário autenticado.')
    } catch (error) {
        return res.status(500).json('Erro interno do servidor')
    }
}
```

## Criação de Token

Vamos usar a biblioteca `jsonwebtoken`. Documentação [aqui](https://www.npmjs.com/package/jsonwebtoken).

```
npm install jsonwebtoken
```

Para gerar um token:

```
jwt.sign(payload, secretOrPrivateKey, [options, callback])
```
> `payload` é o que identifica o usuário. Pode ser o ID ou email, por exemplo.

> `secretOrPrivateKey` é uma senha secreta. Vamos armazená-la em um outro arquivo `senhaJwt.js`

> Passamos o tempo de expiração do tokem em `options`

Exemplo:

```
const login = async (req, res) => {
    const { email, senha } = req.body
    try {
        // checando se o usuário se encontra no banco de dados
        const usuario = await pool.query(`select * from usuarios where email = $1`, [email])
        if (usuario.rowCount < 1) {
            return res.status(404).json({ mensagem: 'E-mail ou senha inválidos.' })
        }
        // checando a senha
        const senhaValida = await bcrypt.compare(senha, usuario.rows[0].senha)  // compara a senha informada pelo usuario com  hash que está armazenada no banco de dados
        if (!senhaValida) {
            return res.status(400).json({ mensagem: "E-mail ou senha inválidos." })
        }
        // gerando token
        const token = jwt.sign({ id: usuario.rows[0].id }, senhaJwt, { expiresIn: '8h' })
        const { senha: _, ...usuarioLogado } = usuario.rows[0] // retorna todas as informacoes do usuario em outra variavel, menos a senha para ser passado pro front.
        return res.json({ usuario: usuarioLogado, token })
    } catch (error) {
        return res.status(500).json('Erro interno do servidor')
    }
}
```

## Verificação do token

Exemplo de verificação de token para dar acesso a listagem de um banco de dados. Não é recomendado enviar o token pelo body. Ao inves disso, vamos recuperar do cabeçalho (**header**) no formato Bearer token.

```
const listarCarros = async (req, res) => {
	// recuperando o token do header do Bearer token
	const { authorization } = req.headers;
	// verificando se o tokem foi informado
	if (!authorization) { return res.status(401).json({ mensagem: "Não autorizado." }) }
	// retirando apenas o token do authorization
	const token = authorization.split(' ')[1]
	try {
		const tokenUsuario = jwt.verify(token, senhaJwt)
		const { rows } = await pool.query('select * from carros')
		return res.json(rows)
	} catch (error) {
		return res.status(500).json('Erro interno do servidor')
	}
}
```

## Verificação do token usando middlewares

Criar no arquivo `./intermediarios/autenticacao.js` a funcao que verifica se o usuario está logado:

```
const jwt = require('jsonwebtoken')
const senhaJwt = require('../senhaJwt')
const pool = require('../conexao')

const verificarUsuarioLogado = async (req, res, next) => {
    // recuperando o token do header do Bearer token
    const { authorization } = req.headers;
    // verificando se o tokem foi informado
    if (!authorization) { return res.status(401).json({ mensagem: "Não autorizado." }) }
    // retirando apenas o token do authorization
    const token = authorization.split(' ')[1]
    try {
        const { id } = jwt.verify(token, senhaJwt)
        const { rows, rowCount } = await pool.query('select * from usuarios where id  =$1', [id])
        if (rowCount < 1) { return res.status(401).json({ mensagem: "Não autorizado." }) }
        req.usuario = rows[0]
        next()
    } catch (error) {
        return res.status(401).json({ mensagem: 'Nao autorizado' })
    }
}

module.exports = verificarUsuarioLogado
```
Agora voce pode incluir o middleware diretamente na rota:

```
rotas.get('/carro', verificarUsuarioLogado, listarCarros)
```

Outra opção é incluir a funcao `verificarUsuarioLogado()` antes das rotas que pedem autenticação:


```
rotas.post('/usuario', cadastrarUsuario)
rotas.post('/login', login)

rotas.use(verificarUsuarioLogado) // todas as rotas daqui pra baixo vao passar pela verificacao
rotas.get('/perfil', obterPerfil)
rotas.get('/carro', listarCarros)
rotas.get('/carro/:id', detalharCarro)
rotas.post('/carro', cadastrarCarro)
rotas.put('/carro/:id', atualizarCarro)
rotas.delete('/carro/:id', excluirCarro)
```
