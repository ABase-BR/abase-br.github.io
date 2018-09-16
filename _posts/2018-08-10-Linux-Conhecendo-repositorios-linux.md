---
date: 2018-08-10
title: Conhecendo repositórios linux
# Video em contrução
#video_id: _iH8f5alzWA

# Descrição
description: Essa é uma referencia para quem está começando a usar o linux e começando a trabalhar com repositórios.

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

## apt e apt-get
**APT** é um conjunto de ferramentas usadas pelo **GNU/Linux Debian** e suas respectivas derivações, entre eles o Ubuntu, para administrar os pacotes .deb de uma forma automática.

O apt-get é um interface simples de linha de comandos para obter e instalar pacotes.



## sources.list
Onde fica a sources.list ?
```sh
/etc/apt/sources.list
```


Como parte de sua operação, o **Apt** utiliza um arquivo que lista as 'fontes' das quais os pacotes podem ser obtidos. Este arquivo é **/etc/apt/sources.list**.

As entradas neste arquivo normalmente seguem este formato:

```sh
deb http://sítio.exemplo.com/debian distribuição componente1 componente2 componente3
deb-src http://sítio.exemplo.com/debian distribuição componente1 componente2 componente3
```

Obviamente, as entradas acima são fictícias e não devem ser usadas. A primeira palavra em cada linha, deb ou deb-src, indica o tipo de arquivo: se ele contem pacotes binários (deb), isto é, os pacotes pré-compilados que nós normalmente usamos, ou os pacotes-fonte (deb-src), que são os ?fontes originais do programa mais o arquivo de controle do Debian (.dsc) e o deff.gz contendo as alterações necessárias para o empacotamento do programa.

No meu caso é
```sh
#

# deb cdrom:[Debian GNU/Linux 8.5.0 _Jessie_ - Official amd64 NETINST Binary-1 $
#deb cdrom:[Debian GNU/Linux 8.5.0 _Jessie_ - Official amd64 NETINST Binary-1 2$

deb http://ftp.br.debian.org/debian/ jessie main
deb-src http://ftp.br.debian.org/debian/ jessie main

deb http://security.debian.org/ jessie/updates main
deb-src http://security.debian.org/ jessie/updates main

# jessie-updates, previously known as 'volatile'
deb http://ftp.br.debian.org/debian/ jessie-updates main
deb-src http://ftp.br.debian.org/debian/ jessie-updates main
#VirtualBox
deb http://download.virtualbox.org/virtualbox/debian jessie contrib

```

Estou usando um sistema Debian 8 (jessie) , dependendo de como você fez sua instalação podemos comentar (ou remover) as primeiras linhas que não referencia ao CD de instalação do Debian.

Após a modificação podemos atualizar nosso repositório.

Todos os pacotes incluídos na distribuição oficial do Debian são livres de acordo com a Definição Debian de Software Livre . Isso assegura o uso livre e a redistribuição de pacotes com seu código fonte completo. A distribuição oficial Debian é a que está contida na seção Main do repositório do Debian.


Como um serviço para os usuários do Debian são providos pacotes em seções separadas que não podem ser incluídas na distribuição main por causa de uma licença restritiva ou problemas legais. São eles:

**Contrib** Pacotes nessa área são livremente licenciados pelo detentor do copyright, mas dependem de outros pacotes que não são livres.


**Non-Free** (estes pacotes foram retirados do Debian a partir do Sarge) Pacotes nessa área apresentam algumas condições na licença que restringem o uso ou redistribuição do software.



## Repositorios
Obter novas listas de pacotes.
```sh
apt-get update
```

Executar uma atualização.
```sh
apt-get upgrade
```

Atualizar a distribuição.
```sh
apt-get dist-upgrade
```

Esses são os comando necessários para sempre manter seu sistema atualizado.


## Instalando programas
Para instalar um pacote vamos usar o **apt-get install** seguido do nome do pacote que queremos instalar.
```sh
apt-get install nmap
```


## Removendo programas
Para remover um pacote vamos usar o **apt-get remove** seguido do nome do pacote.
```sh
apt-get remove nmap
```

Podemos também usar a opção **purge** , ela é responsável por remover pacotes e ficheiros de configuração
```sh
apt-get remove nmap --purge
```


## Instalando pacote no formato **.deb**
Para instalar o pacote no formato **.deb** vamos usar o **dpkg**.

Dpkg é uma ferramenta para instalar, construir, remover e gerenciar pacotes Debian.

Para instalar um pacote
```sh
dpkg -i nomedoarquivo.deb
```

Ou pode ver os arquivos já instalados **.deb**
```sh
dpkg -l
```


## Buscando pacotes
O apt-cache é uma ferramenta de baixo nível utilizada para questionar informação dos ficheiros de cache binários do APT.
```sh
apt-cache search
```

Exemplo básico de uso.
```sh
apt-cache search tor
```
