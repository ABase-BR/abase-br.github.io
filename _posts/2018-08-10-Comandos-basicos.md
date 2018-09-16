---
date: 2018-08-10
title: Linux - Comandos básicos
# Video em contrução
#video_id: _iH8f5alzWA

# Descrição
description: Essa é uma referencia para quem está começando a usar o linux e precisa aprender alguns comandos.

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


## pwd
Mostra o local onde você está atualmente , esse comando é responsável por mostra-nos o caminho por inteiro da diretório em que nos encontramos em dado momento, ou seja um pathname.
```sh
pwd
```



## cd
O comando **cd** te leva a algum diretório , esse comando é responsável por mudar seu diretório atual.
```sh
cd
```

Podemos ver o diretório anterior com o
```sh
cd -
```



Ou podemos usar também o
```sh
cd $OLDPWD
```



## mkdir
O comando **mkdir** cria um **diretório/pasta** .
```sh
mkdir
```



## ls
O comando **ls** lista determinado **local/pasta** , esse comando é responsável por lista o conteúdo de uma diretório, semelhante ao comando dir no MS-DOS
```sh
ls
```

Já com o **ls -a** mostra todos os arquivos , até os ocultos
```sh
ls -a
ls -l
```

O ls é usado para listar determinado lugar , podemos ver um exemplo para listar um diretório
```sh
ls /
```

Podemos ver usado no diretório em que estamos
```sh
ls
```

Podemos também usar o formato de lista longa
```sh
ls -l
```

Para ver arquivos ocultos
```sh
ls -a
```



## touch
Cria um arquivo
```sh
touch
touch teste.txt
```

> Podemos também criar usando ** > **
```sh
   > nomedoarquivo
```



## cat
Mostra o conteúdo de um arquivo, como o comando type do MD-DOS, e é muito usado também para concatenar arquivos.
```sh
cat arquivo.txt
```

Como por exemplo fazendo
```sh
cat a.txt b.txt > c.txt
```

Para juntar o arquivo **a.txt** e **b.txt** num único de nome **c.txt**.



## tac
Ao contrario do **cat** o **tac** monstra o arquivo de forma **inversa**.
```sh
tac arquivo.txt
```



## echo
Imprime na tela/shell
```sh
echo
```

Adicionando nomes com o **>** , caso já tenha algum dado no arquivo será **sobrescrito**
```sh
echo "Júlio" > arquivo.txt
```

Adicionando nomes com o >> , nesse caso ele só é **adicionado** e não sobrescrito.
```sh
echo "Nome" >> arquivo.txt
```

Mais uma vez...
Sobrescreve
```sh
   echo teste > teste.txt  
```

Adiciona   
```sh
echo teste >> teste.txt
```

Vendo o antigo diretório podemos fazer  
```sh
echo $OLDPWD
```



## head
Mostra as primeiras linhas de um arquivo, como por exemplo com **head -10 a.txt**, ou usado como filtro para mostrar apenas os primeiros x resultados de outro comando.

Com o **head** é possível pegar o começo do arquivo , exemplo com o **-n 2** ele pega as duas primeiras linhas.

```sh
head
```

Mostra apenas as duas primeiras linhas do arquivo.
```sh
head -n 2
```



## tail
Funciona de forma inversa ao comando **head**, mostra-nos as últimas linhas de um arquivo ou mesmo do output de outro comando, quando usado como filtro.
```sh
tail
```

Com o comando **tail -n 2** ele mostra apenas as ultimas duas linhas do arquivo.
```sh
   tail -n 2
```

Com o comando **tail -f** você vê em tempo real o arquivo e caso foi adicionado algo exibi na hora.
```sh
tail -f arquivo.txt
```



## Man
Man vem de manual , exemplo.
```sh
man echo
man nmap
```



## rmdir
Ele é responsável por excluir pastas **vazias**.
```sh
rmdir
```



## rm
Apaga arquivo e não **diretório**.
```sh
rm
```

Já o **rm -rf** apaga arquivos e diretórios.
```sh
rm -rf
```

Nesse caso o **r** é de recursive , e o **f** de force.
Qualquer duvida faça **--help**
```sh
rm --help
```



## update-rc.d
**Update-rc.d** serve para adicionar e remover os script que serão inicializados no boot .

Vamos dar um exemplo **desabilitando** o serviço de ssh inicializado no **boot**.

**Desabilitando**
```sh
update-rc.d ssh disable
```

**Habilitando**
```sh
update-rc.d ssh enable
```



## clear
Limpar a tela
```sh
clear
```

ou o atalho
```sh
   Ctrl + l
```
