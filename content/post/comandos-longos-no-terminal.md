+++
title = "Uma forma pratica de editar linhas de comando longas no terminal"
description = "Tutorial rápido de como usar um editor de texto para editar linhas de comando no terminal"
tags = ["Terminal"]
date = "2018-07-08T06:45:14Z"
+++

{{< youtube H-zi2YvrysM >}}

Para editar linhas de comando longas de forma mais conveniente você pode usar seu editor de texto favorito, para isso basta usar o atalho *^xe* (*mantenha a tecla `control` pressionada enquanto pressiona as teclas `x` e depois `e`)*

Caso queira usar outro editor basta preencher a variável *EDITOR*

Por exemplo:

```console
EDITOR=nano
```

Outra coisa importante é tomar cuidado se o seu editor gera arquivos de backup ou cache, pode ser uma boa ideia desabilitar esse recurso para evitar que ele faça isso e acabe gerando arquivos perdidos no seu diretório temporário, sem contar a possibilidade de falha de segurança e de ele restaurar o comando antigo atrapalhando seu trabalho no terminal.
