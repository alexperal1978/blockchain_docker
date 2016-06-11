# blockchain_docker

Criando sua blockchain privada:

É necessário criar 2 nós para o teste. Instalei 2 servidores ubunto com o Docker.


1. Criando a blockchain (isto tem q ser feito em ambos os nós):

Com o ubunto já em funcionamento em modo root ou su, acesse um deles para ser o nó 1 e rode os comandos, vou chamar a blockchain de "chain1":

multichain-util create chain1


Inicialize sua blockchain:

multichaind chain1 -daemon


O endereço gerado servirá para o segundo nó (linux) acessar sua chain1.


2. Conectando (use o endereço fornecido acima no nó 1 para usar no nó 2):


multichaind chain1@172.17.0.2:9723

Uma mensagem de permissão será dada, copie o código da wallet e rode o comando abaixo no primeiro nó:

multichain-cli chain1 grant <codigo> connect


Tente conectar novamente no segundo nó:

multichaind chain1 -daemon

node started significa que já está rodando.

3. comandos em modo interativo para não digitar multichain-cli chain1 para todo comando:


multichain-cli chain1

Segue uma lista de comandos que podem ser dados no modo interativo:

getinfo
help
listpermissions
getnewaddress
getaddresses
getblockchainparams
getpeerinfo


4. usando e trafegando ativos:

No primeiro nó, de o comando:
listpermissions issue

Copie e cole o código do issue no comando abaixo para criar um ativo com 1000 unidades que será dividida em 100 partes de 10:


issue <codigoissue> asset1 1000 0.01

VErifique em ambos os nós se o asset1 criado acima aparece:

listassets

Cheque o saldo em ambos os nós:

gettotalbalances

No primenro nó, mande 100 unidades p/ a wallet do segundo nó:

sendassettoaddress <codigoissue> asset1 100

Vai dar um erro de permissão, ainda no nó 1 garanta a permissão:

grant <codigo> receive,send

Tente novamente:

sendassettoaddress <codigoissue> asset1 100


Cheque novamente o saldo:

gettotalbalances 0

Você também pode checar a transação em cada nó:

listwallettransactions 1


Pronto! Você já consegue enviar e receber moedas de um nó p/outro!
