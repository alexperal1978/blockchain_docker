# Criando sua Blockchain!

# Montando o amiente

Depois de instalar o Docker, abrir com o Kitematic

Adicionar no +new, uma máquina virtual ubuntu-upstart Oficial

Após criada, entrar no container como root;

docker exec -it 70210857c0a4 bash

Atualizar sua maquina vistual com apt-get update;

Instalar o nano com apt-get;

Instalar o git com apt-get;

Instalar o nodejs apt-get install nodejs;

P/ checar se o node foi instalado root@70210857c0a4:/# nodejs -v
v0.10.25
A versão tem que aparecer.

Instalar o npm;

# Para fazer o download do multichain:

cd /tmp
wget http://www.multichain.com/download/multichain-1.0-alpha-21.tar.gz
tar -xvzf multichain-1.0-alpha-21.tar.gz
cd multichain-1.0-alpha-21
mv multichaind multichain-cli multichain-util /usr/local/bin

# Criação do blockchain

multichain-util create chain2

Altere os privilégios de acesso do arquivo params.dat, dentro da pasta do blockchain criado.

~/.multichain/chain2# nano params.dat

Altere as seguintes entrada p/ true:

Global permissions

anyone-can-connect = true              # Anyone can connect, i.e. a publicly readable blockchain.
anyone-can-send = true                 # Anyone can send, i.e. transaction signing not restricted by address.
anyone-can-receive = true              # Anyone can receive, i.e. transaction outputs not restricted by address.
anyone-can-issue = true                # Anyone can issue new native assets.

Mais abaixo, anote a porta RPC

default-rpc-port = 6808

Após salvar as alterações, recupere as informações de RPC do arquivo multichain.conf

cat multichain.conf
rpcuser=alex
rpcpassword=teste

Agora sim, podemos iniciar nossa blockchain

multichaind chain2 -daemon -rpcuser=multichainrpc -rpcpassword=DA7tMWRBqdtQmyo8f5TQ9K2mbZkP9YUhmjHB3ssM553

DEve aparecer uma mensagem como abaixo:

MultiChain Core Daemon build 1.0 alpha 21 protocol 10005

MultiChain server starting
Looking for genesis block...
Genesis block found
New users can connect to this node using
multichaind chain2@172.17.0.3:6809

Node started --> isto significa que funfou!

# Agora vamos p App

Vamos baixar uma imagem de uma App teste do Git.

Vamos criar as chaves para acessar o Git:

ssh-keygen -t rsa -b 4096 -C "alex.peral@yahoo.com.br"

Ele irá perguntar se deseja armazenar em algum local específico e se deseja uma senha:

Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
Created directory '/root/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
00:ca:c0:31:e7:81:89:00:4f:3c:0e:b5:4d:30:12:d4 alex.peral@yahoo.com.br
The key's randomart image is:
+--[ RSA 4096]----+
|%BX+o            |
|oX*E..           |
| o=o. .          |
|  .    .         |
|        S        |
|                 |
|                 |
|                 |
|                 |
+-----------------+

PAra checar se funcionou:

eval "$(ssh-agent -s)"
Agent pid 1808

Para pegar a chave e colocar no seu GitHub:

ssh-add ~/.ssh/id_rsa

cat /root/.ssh/id_rsa.pub

Vai retornar uma parada assim:

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCyV8y8LjJk3fVSaH0ZFx9gQJDEqvqi+tUcj8B37CYPUeR1SGiBgS0WmEFux/q9KWdPlNQDJQOlXS5cyH4InLN+4feu5cVtLqtFB54Fh5wKu4KY+yL4O7aosXh/JbFeMwtpS0ev9r61Cczm5gNPNLDglbsbmHKI3O9xDNIVroauHMLUFw+MO2uSIypYI8Yrf4IomMnHHq/eAwycg+bmRiqXfZHHklS2NF47iLphJY04w4Ot2fcjTXuKWvXyZZiwi/zEwZs64vAwzO4qcBnN0iQT7rsDsnZVjufcMgTpe89Qt0O8btLXOV7ELuXQ7JwosnGnkzDZ9zrXxZiFeFSoeiXWPcM15pzSnI1iktcmNSU0BSLL7zl05O4Bx1MwbXJWlNmyDtNtmboHOefeKQSON5gCXmCzunz1lkvjH4Urqhe9RT6PvdwhVjx4ZUwjxF4f3SUOCOhkoW+5ylqNdmhlvSrJM+hC+rWT3r24UkxtJlLUAf+/cyJc6GGCwB6TAH7wJyr5uUyy2w8KF+niFuk+EuCC3f4Cq+aSlRoLBL81/oD0TDkGkHFhwpa8WhUN2uIbBqkTehXOGje7ZB0UQNGXKYqmNVfNC6xWPHhj1dJs+q0uWx34sZ3v6jYRVsP/DsoB9rhy0y8URhXExjQC4LY9jW6CO5tFRNHzYcKuIw71/t+KWQ== alex.peral@yahoo.com.br

# Agora vamos baixar o app teste:

DEvemos instalar o multichain-node

npm install multichain-node --save

PAra baixar o app:

git clone git@github.com:scoin/multichain-node.git

Pode baixar p qualquer diretório. Após, deve-se entrar no diretório do App e executar:

npm install
npm test

Test é a nossa App, navegando pelos diretórios, pode-se chegar ao arquivo test.js, ao editá-lo, é possível alterar a porta RPC, user e senha. Isto precisa ser alterado p/ funcionar.



