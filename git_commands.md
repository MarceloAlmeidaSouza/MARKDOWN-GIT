# Linhas de comandos git
[Git documentação](https://git-scm.com/docs/git/pt_BR)

### Git workflow
---
* Inicia um diretório gerenciável pelo git, o comando executado na pasta atual irá torná-la gerenciável pelo git.
  * **git init** 
  
* Defini a url do repositório remoto, importante para realizar o push das alterações locais para o ambiente remoto.
  * **git remote add origin [remote-git-url]**
  
* Estabelece a conexão com o repositório do branch remoto na condição de que o repositório exista, usado ao inicializar o ambiente do branch master, conecta o ambiente local com o remoto
  * **git push --set-upstream origin master**
  
* Estabelece a conexão com o repositório remoto na condição de que o repositório exista remotamente, usado na criação de um novo branch
  * **git branch --set-upstream-to=origin/remote_branch_name local_branch_name**
  
* Clona o diretório da url ou path
  * **git clone `https://some.url/file.git`** 
  * **git clone `file_path/file.git`**
  
* Retorna o nome do branch atual
  * **git branch**
  
* Retorna uma lista de branches do projeto atual com a key do commit e o branch remote
  * **git branch -vv**
  
* Lista todos os branches remotos e os respectivos configurados localmente se houver.
  * **git remote show origin**
  
* Cria um novo branch e realiza o checkout/switch últil para verificar se branch local possui um branch remoto
  * **git checkout -b new_branch_name**
  
* Envia os commits do repositório local para o repositório remoto, [current_branch_name] geralmente os branches local e remoto tem o mesmo nome.
  * **git push -u origin [current_branch_name]**
  
* Exclui um branch, com d minusculo caso exista pendencias no branch aparecerá uma mensagem de alerta
e com d maisculo o branch será excluído sem apresenta esta mensagem
  * **git branch -d branch_name**
  * **git branch -D branch_name**

* Lista as configurações do repositorio corrente.
  * **git config --list**

* Adiciona as configurações de usuário ao repositório.
  * **git config user.name 'User Name'**
  * **git config user.email 'blabla@bla.com'**
    
### Untracked Files/Folders
---
* Lista os arquivos untracked antes de executar um comando de exclusão de arquivos, não precisa de add, commit, push.
  * **git clean -n**

* Exclui arquivos untracked onde [-- path_file]([] de opcional) indica qual arquivo excluir, não precisa de add, commit, push.
  * **git clean -f [-- path_file]**

* Exclui pastas untracked onde [-- path_folder]([] de opcional não incluir quando usar os opcionais) indica qual pasta excluir
    * **git clean -fd [-- path_folder]**

### Tracked Files
---
* Compara as diferenças de um arquivo entre dois branchs
    * **git diff branch_a branch_b -- path_file**

* Realiza o commit de um arquivo especifico 
    * **git commit -m "My commit description" path_file**

### Git Solutions
* Error: cannot lock ref 'refs/remotes/origin/[branch_name]': is at [commit_number] but expected [commit_number]
* Ocorre quando temos dois branchs com o mesmo nome, no entanto a diferença entre os nomes está no sensitive case ou sejan
* branch_ABC == branch_abc, geramente este erro ocorre no windows.
    * **git update-ref -d refs/remotes/origin/[branch_name]**


* converte o branch corrente deixando igual ao branch master
    * **git reset --hard master**

* realiza diff do branch atual com um branch remoto
    * **git fetch; git diff ..origin/branch_name**

* realiza um merge sem executar o commit (-n) no branch atual, [commit-hash] a hash do commit almejado.
    * **git cherry-pick -n [commit-hash]**

* realiza um merge sem executar o commit (-n) no branch atual, [commit-hash-older]^..[commit-hash-recently] hash do commit mais antigo (^ opcional inclusivo) (..) até a hash do commit mais recente, ou seja desde do commit mais antigo até o mais atual incluindo todos os commits entre eles.
    * **git cherry-pick -n [commit-hash-older]^..[commit-hash-recently]**

* realiza um merge sem executar o commit (--no-commit), aplica as hashes individualmente o seja, apenas as indicadas. 
    * **git cherry-pick --no-commit [commit-hash-first] [commit-hash-sencond] [commit-hash-third]**

* aplicacao de patch
    * **git apply C:\Users\Lenovo\Desktop\cejam\icejam\patches\dev_cris-prestacao.patch --ignore-whitespace --ignore-space-change --reject --whitespace=fix**

* gera uma patch a partir de um commit 
    * **git format-patch -1 [commit-hash]**


    
Inicia um repositorio
git init

tracked, staged
git add

Retorna os 2 ultimos commits
git log -n(2)

Retorna em linhas os 2 ultimos commits
git log --oneline -n

Comando utilizado para retorna arquivo adicionado para o estado de untracked
git restore --staged <file>...

Remove as edições do arquivo retornando para o seu último estado de edição
git restore <file>

Remove as edicoes dos arquivos, ainda mesmo que tenha entrado no estado --staged, ou seja adicionados para commit,
retornando para o seu último commit.
git reset HEAD --hard

Desfaz as alterações do ultimo commit
git reset HEAD^ --hard

Lista as configurações do repositorio corrente.
git config --list

Adiciona configurações de usuário ao repositorio.
git config user.name 'Nome do usuario'
git config user.email 'blabla@bla.com'

Lista os branches do projeto
git branch

Cria um novo branch chamado funcionalidadeA
git branch funcionalidadeA


Alterna da branch atual para a branch funcionalidadeA
git checkout funcionalidadeA

Exclui um branch, com d minusculo caso exista pendencias no branch aparecerá uma mensagem de alerta
e com d maisculo o branch será excluído sem apresenta esta mensagem
git branch -d nomedobranch
git branch -D nomedobranch

Adiciona as alterações commited no branch alvo ao branch corrente
git merge nomedobranch


Cria um novo branch ja com checkout
git checkout -b nomedonovobranch


git rebase nomedobranch

Clona o projeto git
git clone path 

Baixa os arquivos sem realizar o merge ou rebase, utilizar o git rebase sem o nomedobranchalvo para fazer o merge dos arquivos
git fetch && git rebase

Git pull equivalente ao git fetch + git rebase
git pull

Git bare criar um diretorio centralizador de projeto o qual é o distribuidor central
git init --bare

Envia os commits para a central, no caso para o projeto bare
git push

Adiciona uma tag para versionamentos estavéis
git tag v1.0
git push origin v1.0

Exclui a tag local e a tag remota no repositorio bare
git tag -d v1.0
git push --delete origin v1.0

Muda para a tag v1.0
git checkout v1.0

Cria um branch para editar a tag v1.0
git switch -c correcao-tag-v1.0

Faz registro do repositorio remoto no ambiente local
git remote add origin https://github.com/MarceloAlmeidaSouza/geek-git1.git

Envia para o servidor remoto o commit
git push -u origin master

Consulta se existe algum repositorio remoto registrado
git remote -v

Salvar as credenciais salvando as em um proximo login
git config credential.helper store

Retorna todos os arquivos para seu status original
git checkout -- .

Retorna o arquivo para seu status original
git checkout -- arquivo1.html
git restore arquivo1.html

Retorna para o estado unstaged um arquivo no estado staged post command git add filename
git restore --staged arquivo1.html

Retorna para o estado do ultimo commit um ou muitos arquivos
git checkout HEAD -- .
git checkout HEAD -- filename


Remove o ultimo commit, e realiza commit no revert
git revert key do ultimo commit
git push -u origin branchname

Comando para exclusão local da quantidade de commits representados por [n], lembrando que começa do mais recente.
git reset HEAD^[n]


Retorna a diferença do arquivo no estado atual com o arquivo no estado do commit previsto no HEAD~[numero do commit, não id do commit],
observação remover[]
git diff HEAD~[n] path/file.ext


Remove todos os arquivos tracked not staged exceto -- !:file_path
git restore  -- :!app/webroot/index.php

Adiciona todos os not staged arquivo para o status staged excel [-- :!file_path]
git add -u -- :!app/webroot/index.php

Lista todos os arquivos no status not staged, arquivo tracked modificados
git ls-files -m

Lista todos os arquivos untracked com exceção dos arquivos ignorados no arquivo .git
git ls-files --others --exclude-standard

Historico grafico das alterações de um dado arquivo gerenciado pelo git
gitk path/file.ext
# The largest heading
