+++
date = "2018-09-09T08:19:09-03:00"
description = "Como configurar chaves ssh para acessar seus servidores de forma mais segura"
tags = ["Segurança", "UNIX"]
title = "ssh usando chaves de acesso"
topics = []

+++

{{< youtube f-4R_PNEFT4 >}}

Acessar servidores via ssh usando um conjunto de chaves publica/privada é mais seguro e pratico principalmente mais seguro, alem de facilitar a automação de várias tarefas.

## Criando as chaves

Primeiro crie as chaves com o seguinte comando:

```console
mkdir ~/.ssh
ssh-keygen
```

Precisa fazer isso apenas uma vez na maquina cliente e um conjunto de chaves será gerado, você pode definir o nome do arquivo que por padrão seria `id_rsa` para a chave secreta e `id_rsa.pub` para a chave publica.

É interessante criar uma chave para cada servidor que pretende acessar assim como é aconselhável gerar senhas para cada serviço, mas no caso das chaves você esta no controle de metade da chave, a parte secreta, essa precisa ficar bem protegida.

## Copiando a chave publica para o servidor

É necessário copiar a chave que acabamos de gerar para o arquivo `~/.ssh/authorized_keys` no servidor. Você pode fazer isso manualmente usando os seguintes comandos.

```console
cat ~/.ssh/id_rsa.pub |
ssh usuário@exemplo.com.br 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
```

Mas é mais fácil usar o comando `ssh-copy-id` que praticamente faz a mesma coisa, veja o exemplo.

```console
ssh-copy-id -i ~/.ssh/id_rsa.pub usuário@exemplo.com.br
```

Com qualquer um dos dois comandos o diretório `.ssh` sera criado no home do usuário no servidor e essa vai ser a ultima vez que você precisou digitar a senha para acessar esse terminal.

## Ainda mais pratico

Você pode parar no comando anterior, o servidor já esta aceitando suas conexões ssh sem pedir a senha porque estamos usando um conjunto de chaves publica/privada. Mas podemos tornar as coisas ainda mais fáceis.

Edite o arquivo `~/.ssh/config` como no exemplo abaixo.

```
Host *
    ServerAliveInterval 240
    ConnectTimeout 0

Host exemplo
    HostName exemplo.com.br
    Port 22
    User nome_usuário
    IdentityFile  ~/.ssh/id_rsa
    IdentitiesOnly yes
```

Com isso você esta configurando o ssh para não desconectar por inatividade o que ajuda bastante quando se esta programando e é preciso ficar muito tempo indo e voltando entre seu terminal e outras ferramentas. Também estamos configurando o nome do usuário, a porta e um apelido para o servidor, dessa forma no lugar de digitar `ssh voce@exemplo.com.br` basta digitar `ssh exemplo`. Essa pequena economia de teclas faz toda diferença e também previne erros.

## Segurança

Esse tipo de configuração é mais segura que usar apenas uma senha desde que você cuide bem do seu conjunto de chaves.
