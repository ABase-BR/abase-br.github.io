---
date: 2018-08-10
title: Manipulando usuários
# Video em contrução
#video_id: _iH8f5alzWA

# Descrição
description: Essa é uma referencia para quem está começando a usar o linux e precisa aprender alguns comandos para a manipular usuários Linux.

# Categoria
categories:
  - linux

#Arquivos a ser compartilhado
#resources:
#  - name: Source code
#    link: https://github.com/CloudCannon/creative-jekyll-theme/
#  - name: CloudCannon
#    link: https://cloudcannon.com
#type: Video

# Tipo de arquivo
type: Document

#set: getting-started
#set_order: 1

#Inicia POST
---

## Manipulação de Usuários
Aqui vamos aprender o necessário para manipular e gerenciar seus usuários.

## Super usuário

Assim como o administrador do Windows o **Linux** também tem o seu mais com o nome diferente. O nome de administrador no Linux se chama **root** , ele é o super usuário , tem total poderem no sistema (isso é ruim pois pode danificar seu sistema) recomendo o uso do comando **sudo**.

**Como identificando root**
Quando você esta logado como **root** no terminal fica com
 #

Quando você está com um usuário comum fica com
 $


## adduser
Comando responsável por adicionar um usuário.
```sh
adduser teste
```
> Não esqueça de aceitar no final para ser criado o **usuário**.



## Arquivo passwd
> O arquivo que fica todos os usuários do Linux é o **passwd** podemos ver o arquivo com o cat
```sh
 cat /etc/passwd
```

Nesse arquivo podemos ver os usuários , grupo de usuários , pasta do usuário e se ele tem acesso a **bash**.

Usuários que tem
```sh
 /bin/bash
```
Podem se conectar com o terminal

Usuários que tem
```sh
 nologin
 usr/sbin/nologin
```

Eles não podem fazer login no sistema

Usuários que possuem
```sh
 /bin/false
```
Geralmente são serviços do sistema que não podem fazer login no sistema , esse usuário não pode logar em um terminal.


## usermod
Este comando modifica uma conta de usuário do sistema. Nesse caso vamos usar o usuario **teste**.
```sh
usermod -s /bin/bash teste
```
faz com que o shell padrão do usuário aluno passe a ser o /bin/bash.

Vamos trocar o nome do usuário **teste** para **teste2**.

```sh
usermod -l teste2 teste
```

Podemos ver que o diretório do **teste2** ainda se chama **teste** , vamos mudar.
```sh
usermod -d /home/teste2 teste2
```

## deluser
Deleta usuário
```sh
 deluser teste
```

Mais podemos ver que ainda vamos ter o diretório do usuário , para isso precisamos usar **--remove-home**.
```sh
deluser teste2 --remove-home
```


## useradd
Adiciona usuário igual ao **adduser** .

**Definindo diretório**
```sh
-d /home/diretorio-usuario
```

**Definindo acesso a shell**
E se ele vai ter acesso a uma shell usamos **-s** e seguido pelo nome do usuário.
```sh
-s usuario
```

Criando usuário **Tiao**.
```sh
useradd -d /home/tiao -s /bin/bash tiao
```

Ou podemos definir como false para ele não ter acesso a **shell**.

```sh
 useradd -d /home/tiao -s /bin/false tiao
```

No final não será pedido uma senha então será necessário usar o comando **passwd**


## Listando usuários
O arquivo em que fica gravado todos os usuarios é o **/etc/passwd**
Caso queira listar os usuários faça o seguinte comando com a ajuda do **cat**
```sh
 cat /etc/passwd
```

## Mudando usuário 
Você esta usando seu usuário normal na sua maquina e deseja entrar como **root** ? Simples..
```sh
 su
```

Em seguida digite sua senha.
Ou você está usando o usuariox e deseja mudar para usuarioz
```sh
 su usuarioz
```

## passwd
Mudar a password do nosso utilizador/usuário logado.
```sh
passwd
```



## sudo
Adicionando usuário tiao ao grupo **sudo**
Primeiro entre com um usuário que tenha poderes como o **root** em seguida digite
```sh
adduser tiao sudo
```

Eu pessoalmente prefiro dar um reboot na maquina em seguida já está tudo **OK**.
Para usar é simples , com um usuário normal você não pode dar o comando **ifconfig** , mais com o **sudo**.
```sh
 sudo ifconfig
```

Você também pode retirar o poder de sudo de um usuário da seguinte forma.
```sh
 deluser tiao sudo
```

Após fazer isso tente novamente usar o **sudo**.

Vai dar um erro , esse erro você pode ver em **/var/log/auth.log**.

```sh
 cat /var/log/auth.log
```
Nesse arquivo você também pode adicionar usuário ao grupo sudo.
```sh
 /etc/sudoers.d
```

Eu prefiro usar o editor **nano** , mais pode usar qualquer um da sua escolha.
```sh
 nano /etc/sudoers
```

Adicione seu usuário abaixo na seguinte linha (nesse caso meu usuário se chama **greenmind**).
```sh
# User privilege specification
 root    ALL=(ALL:ALL) ALL
 greenmind    ALL=(ALL:ALL) ALL
```

Não esqueça de salvar para sair.

> Esse arquivo só pode ser modificado se seu usuário tiver privilegio igual administrador.
