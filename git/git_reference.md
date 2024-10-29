
# Referência de Comandos Git

Este documento serve como uma referência rápida para os comandos Git discutidos.

## Configurações de Ambiente

- `git config --global user.name "Seu nome"`  
  Configura o nome do usuário globalmente.

- `git config --global user.email "Seu email"`  
  Configura o e-mail do usuário globalmente.

- `git remote add <nome_repositorio> <url>`  
  Adiciona um repositório remoto ao seu repositório local, permitindo buscar ou enviar mud
  **Exemplo:**  
  ```bash
  git remote add colega /caminho/para/repositorio/do/colega
  ```

## Comandos Básicos

- `git init`  
  Inicializa um repositório Git vazio.

- `git clone <url>`  
  Clona um repositório remoto.

- `git add <arquivo>`  
  Adiciona um arquivo específico ao staging.

- `git add *`  
  Adiciona todos os arquivos ao staging.

- `git commit -a`  
  Abre o editor de texto para escrever uma mensagem de commit.

- `git commit -m "mensagem"`  
  Faz o commit com uma mensagem direta no terminal.

## Manipulação de Commits

- `git reset <hash_commit>`  
  Desfaz um commit específico.

- `git reset --hard HEAD~1`  
  Reverte o último commit, apagando as alterações permanentemente.

- `git clean -f -d`  
  Apaga todos os arquivos não rastreados.

- `git checkout -- <arquivo>`  
  Remove alterações não comitadas de um arquivo específico.

- `git reset HEAD^ --soft`  
  Desfaz o último commit, mantendo as alterações.

- `git cherry-pick <commit>`  
  Aplica um commit específico de outra branch na branch atual.  
  **Exemplo:**  
  ```bash
  git checkout main
  git cherry-pick <commit-hash>
  ```

- `git commit --amend`  
  Corrige o último commit, permitindo modificar a mensagem.

- `git rebase -i HEAD~<n>`  
  Junta ou edita commits interativamente, onde `<n>` é o número de commits para ajustar. 

- `git rebase <branch>`  
  Reaplica os commits da sua branch atual no topo dos commits de outra branch.

- `git reset --hard <hash_commit>`  
  Reseta para um commit específico e envia para o repositório remoto.  
  **Exemplo:**  
  ```bash
  git reset --hard <commit_hash>
  git push -f origin <branch>
  ```

## Visualização e Histórico

- `git status`  
  Mostra o estado atual do repositório.

- `git log`  
  Exibe o histórico de commits.

- `git log -p`  
  Exibe o histórico detalhado dos commits.

- `git diff <commit>`  
  Exibe as diferenças entre um commit específico e o atual.

## Manipulação de Branches

- `git branch`  
  Lista todas as branches locais.

- `git branch -r`  
  Lista todas as branches remotas que foram baixadas.

- `git branch <nome_branch>`  
  Cria uma nova branch.

- `git branch -d <nome_branch>`  
  Deleta uma branch.

- `git checkout <nome_branch>`  
  Altera para uma branch específica.

- `git checkout -b <nome_branch>`  
  Cria e troca para uma nova branch em um único comando.

- `git checkout -b <new-branch> <remote>/<branch>`  
  Cria uma nova branch local com base em uma branch remota.

- `git merge <branch>`  
  Mescla outra branch na branch atual, preservando o histórico completo.  
  **Exemplo:**  
  ```bash
  git checkout main
  git merge feature-branch
  ```

- `git branch -m <novo_nome>`  
  Renomeia a branch atual.

## Sincronização com Repositórios Remotos

- `git push origin <branch>`  
  Envia as mudanças para o repositório remoto.

- `git fetch`  
  Baixa atualizações do repositório remoto sem mesclar automaticamente.

- `git pull`  
  Baixa e aplica atualizações do repositório remoto.

- `git bundle create <file.bundle> --all`  
  Cria um arquivo `.bundle` com todo o histórico do repositório.

- `git fetch <file.bundle> <branch>`  
  Importa commits e branches de um arquivo `.bundle`.

## Outros Comandos Úteis

- `git restore --staged <arquivo>`  
  Remove um arquivo do staging.

- `git reset <arquivo>`  
  Desfaz o staging de um arquivo específico.

- `git clean -n -f <caminho>`  
  Lista arquivos não rastreados no diretório especificado.

- `git ls-files --cached`  
  Lista todos os arquivos commitados, incluindo os ocultos.

- `git checkout -- <arquivo>`  
  Desfaz alterações em um arquivo específico e o remove do staging.

- `git diff`  
  Mostra as diferenças entre o último commit e o commit atual (`HEAD`).

## Exemplo de Alteração de Mensagem de Commit Específico

1. Inicie uma rebase interativa no commit anterior:  
   ```bash
   git rebase --interactive <hash_commit>^
   ```
2. No editor, altere `pick` para `edit` no commit desejado.
3. Modifique a mensagem:  
   ```bash
   git commit --amend
   ```
4. Continue o rebase:  
   ```bash
   git rebase --continue
   ```
