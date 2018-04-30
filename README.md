# Ethereum — Configurando uma rede privada com geth (MAC)
Este é um passo a passo, escrito de maneira simples e informal, para que qualquer pessoa possa acompanhar, até mesmo quem não é um programador experiente.

Para que este tutorial possa ser executado é necessário ter o geth instalado em seu computador.

Abra o terminal 

Crie um diretório

      $ mkdir eth4

Crie uma conta neste diretório

      $ geth — datadir ~/eth4 account new

Escolha uma senha que você não vá esquecer, e confirme a senha

Após a criação da conta, copie o endereço.

Por exemplo: Address: {fa1c6d541679377a9f6ba72d7caf4362bc412d41}

Crie o arquivo genesis.json

      $ vi ~/eth4/genesis.json

Copie e cole o código abaixo

      {

           “config”: {

           “chainId”: 15,

           “homesteadBlock”: 0,

           “eip155Block”: 0,

            “eip158Block”: 0

       },

            “gasLimit”: “210000”,

            “difficulty”: “20000”,

             “alloc”: {

             “USE O ADDRESS AQUI”: {

             “balance”: “1000000000000000000000000000”

          }

        }

      }

Digite :wq para salvar o arquivo genesis.json

Inicialize a rede privada, digite:

      $ geth — datadir ~/eth4 init ~/eth4/genesis.json

Crie um endpoint, digite:

      $ geth — datadir ~/eth4 — networkid 9000

OBS: Esse numero definido como 9000 pode ser qualquer numero acima de 10.

Abra uma nova aba do terminal e digite:

      $ get attach ipc:/Users/tell/eth4/geth.ipc

Agora usando o console, liste as contas que existem neste nó Ethereum

      > personal.listAccounts

Vamos verificar o saldo da conta

      > eth.getBalance(“ADDRESS AQUI”)

para iniciar o processo de mineração, digite:

      > miner.start()

Aguarde algum tempo, 1 minuto está bom, e pare o processo de mineração. digite:

      > miner.stop()

Agora vamos criar uma nova conta, digite:

      > personal.newAccount()

Vamos conferir as contas, digite:

    > personal.listAccounts

Vamos verificar o Balance da nova conta, copie a conta e substitua no comando abaixo:

    > eth.getBalance(“ADDRESS”)

Vamos verificar o Balance da conta original, copie a conta e substitua no comando abaixo:

    > eth.getBalance(“ADDRESS”)

Vamos desbloquear a conta para poder fazer transações.

    > personal.unlockAccount(“ADDRESS”)

Vamos criar uma transação

     > eth.sendTransaction({from: eth.accounts[0], to: eth.accounts[1], value: web3.toWei(0.005, “ether”)})

Agora vamos verificar o balance das contas.

Feito isso estamos com uma rede privada pronta para iniciarmos a criação de Smart Contracts.

Este conteúdo foi adaptado do video: https://www.youtube.com/watch?v=TU8d9Q_Cagg
