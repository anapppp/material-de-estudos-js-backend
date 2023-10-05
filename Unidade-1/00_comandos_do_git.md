# Comandos básicos do GIT

![](https://media3.giphy.com/headers/GitHub/w8ZJLtJbmuph.gif)

Comandos                | Descrição
----------------------- | --------------------------------
`git add .`             | adiciona para o stage todo o diretorio
`git status`            | mostra o status
`git clone`             | clona o diretorio da nuvem pro computador
`git commit`            | salva uma versao do seu projeto
`git commit -m "msg"`   | comita com mensagem
`git push`              | empurra pra nuvem
`git pull`              | puxar para a maquina
`git init`              | inicializa um repositorio no seu computador (local)
`git status`            | fornece o status
`git add file.js`       | adiciona para o stage apenas o arquivo
`git reset file.js`     | remove argit reset ge
`git checkout -b nova-branch`   | sai da branch, cria uma nova e muda
`git switch`            | troca de branch 
`git remote`            | exibe lista de repositórios remotos associados ao repositório local
`git remote add <nome-remoto> <URL-do-repositorio-remoto>` | adiciona um repositório remoto ao seu projeto Git. Usa-se comumente *`origin`* ao iniciar um novo repositório e *`upstream`* para colaborar com um projeto remoto.
`git branch`            | lista as branchs
`git branch -m master main` | altera o nome da branch de master para main
`git commit --amend -m "nova mensagem"` | Altera um commit e atualiza os arquivos que estavam no stage
`git --h`               | Help!
`git remote add upstream https://github.com/REPOSITORIO`  |  para manter seu repositório local atualizado:
`git pull upstream main`  |  baixa e mescla as alterações no seu repositório local com base na branch main deste repositório original 
`git checkout -b feat/community/seunomedeusuario`   |    cria uma nova branch

##  Status no GIT

> **not staged:** quando o usuário alterou arquivos mas não adicionou para o stage 

> **staged:** quando a pasta ou arquivo já foi adicionado ao stage pelo `git add`, e está pronto para comitar 
