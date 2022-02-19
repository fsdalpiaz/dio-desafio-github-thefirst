# Comandos cmd Windows
cd -> change directory
dir -> mostra o que tem na pasta, semelhante ao ls do linux
mkdir -> cria pasta "echo > hello.txt"
del -> exclui itens dentro da pasta
rmdir -> exclui a pasta, se acompanhado dos recursos /S /Q apaga toda a árvore de pastas e arquivos dentro da pasta a ser apagada

# no Unix (linux, apple, etc):
cd
ls -> dir
mkdir
rmdir igual a rm -rf


ls -a -> mostra diretórios ocultos (.algumacoisa/)



## Os três objetos internos fundamentais do Git:
- Blobs ("arquivos"): bloco básico de composição
"bolha", é um objeto que guarda os arquivos do git com seus respectivos metadados (tipo do objeto, tamanho do arquivo, barra contrária e 0 "\0" e o conteúdo do arquivo, seja texto, binário, etc) mas não o nome do arquivo. Ex.: se criptografarmos com o método "git hash-object --stdin" a string "conteudo", echo "conteudo"... o resultado vai ser diferente do que se usarmos o método openssl sha1 diretamente, isso pq o método git hash criptografa o blob e seus metadados junto com o conteúdo, ou seja, se fizermos "echo -e "blob 9\0conteudo | openssl sha1" com o blob e os metadados, "blob 9\0", o hash resultante será o mesmo que pelo método git "git hash-object --stdin".

- Trees ("pastas"): são base para os commits. Armazenam e apontam para blobs diferentes, guardam o nome do arquivo e é responsável por montar toda a estrutura de onde estão localizados os arquivos, podem apontar para blobs/arquivos e outras árvores. É um objeto recursivo. Uma mudança no sha1 da blob consequentemente muda o sha1 da árvore, altera toda a estrutura da encriptação.



- Commits: é o objeto que junta tudo (blobs e trees), dá sentido a alteração que está sendo feita. Ele aponta para uma árvore (tree), para um parente (o ultimo commit realizado antes dele), aponta para o autor e para a mensagem. Tem um carimbo de tempo e possuem sha1 que é o hash de toda essa informação (tree, parente, autor, mensagem, timestamp).

## Gerando chaves SSH

ssh-keygen -t ed25519 -C "e-mail do git"

pastas que começam com ".", ex.: .ssh, são pastas ocultas

para ativar o agente de ssh

eval $(ssh-agent -s)

ssh-add caminho da chave

# Prático:

git init: inicia/cria um repositório do git, aqui o/s arquivo/s do repositório ainda são do tipo Untracked

git add: mover arquivos e dar inicio ao versionamento
A partir do git add o arquivo passa a ser Tracked e passa diretamente ao estágio de "Staged" (Unmodified, Modified e Staged):
- Unmodified é o arquivo a partir do Tracked, ou seja, o arquivo que o git passa a ter ciência da forma como ele é
- Modified é quando esse mesmo arquivo sofreu alguma alteração no conteúdo, ele passa a ser Modified automaticamente, caso façamos um git add novamente esse arquivo passa a ser Staged
- Staged são os arquivos que estão se preparando para fazer "parte do show", ou seja, que estão prontos e prestes a receber um commit e após o commit o arquivo passa a ser Unmodified novamente
- Se removermos o arquivo ele volta a ser Untracked
- git add nomeArquivo
- git add * :adiciona todos os arquivos untracked
- git add . :adiciona todos os arquivos e diretórios untracked


git commit: fazer commit

No git temos dois ambientes:

Ambiente de desenvolvimento: é o ambiente em que temos os arquivos locais, os diretórios de trabalho e Staging area. Você cria os arquivos no diretório local, você faz um git add para passar esses arquivos para Stage e faz git commit para registrá-los no seus repositório local.

Servidor: é onde transferimos a fotografia do código do repositório local para o repositório remoto do git com todas as infos do projeto.


Para exibir as configs do Git:

git config --list

Para alterar alguma info:

git config --global --unset e a info que deseja alterar ex.: user.name, user.email

Para inserir novamente:

git config --global a info que deseja inserir ex.: user.name, user.email

Para enviar arquivos para o repositório:

git push origin main

Para puxar o arquivo do git antes de alterar e fazer push (quando há conflito):

git pull origin main (ou master)

git remote -v -> mostra os repositórios remotos para o qual o repositório local está apontado