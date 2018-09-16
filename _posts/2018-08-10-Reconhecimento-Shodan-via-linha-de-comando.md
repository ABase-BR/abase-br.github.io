---
date: 2018-08-10
title: Shodan via linha de comando
# Video em contrução
#video_id: _iH8f5alzWA

# Descrição
description: Essa é uma referencia para quem está começando a usar o shodan via linha de comando.

# Categoria
categories:
  - reconhecimento
  - OSINT

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

# Shodan via linha de comando (CLI)

## Usando o Linux
### Instalando Shodan
Para instalar o **shodan** temos diversas formas , no site oficial eles recomendam o uso de **easy_install** e é possivel usar tambem o **pip**.

### Instalação via easy_install
**Easy Install** é um gerenciador de pacotes para a linguagem de programação Python.
```sh
sudo easy_install shodan
```

Caso queira instalar a versão mais antiga da biblioteca podemos usar
```sh
easy_install -U shodan
```
> Por padrão ele já vem instalado no Debian e seus derivados.

### Instalando via PIP e PIP3 (Python Package Index)
Podemos usar o **PIP** para o python e o **PIP3** para o python3.

#### Usando PIP
Caso queira instalar o **pip** ,usando apt.
```sh
sudo apt-get install python-pip
```

Podemos instalar agora o pip
```sh
pip install shodan
```

#### Usando PIP3
Eu uso o **pip3** para as minhas instalações , mais todos são iguais.
```sh
apt-get install python3-pip
```

Agora podemos instalar o shodan usando o PIP3.
```sh
pip install shodan
```

## Obtendo Key
Podemos ir até o site do shodan e logar na sua conta como já foi explicado.

```sh
https://account.shodan.io
```

Lá no subdominio **account** vamos obter a nossa **API KEY** para nossos testes.

## Usando sua chave
Devemos inserir a nossa chave para usar o shodan sem problemas.
```sh
shodan init "RPyjZUBjabK1Yld5iKjc8vuPwjPQJDqh"
```

Essa é a minha Key e você deve inserir a sua , ela pode ser reiniciada caso precise.

Se tudo ocorreu bem vamos receber a mensagem **Successfully initialized**.

## Comaçando a explorar com Shodan CLI
Podemos usar o **Shodan** depois de inicializar ele usando **init**.

Vamos ver as opções que temos , podemos usar **--help** ou até **-h**.
```sh
shodan --help
```

E toda opção como por exemplo o **search** , pode ter uma outra opção de **help**.
```sh
shodan search --help
```

## Buscando informações de um determinado host
Podemos buscar informações de um determinado alvo usando o **host** , ele pode trazer informações importantes na hora de um reconhecimento baseado em **OSINT**.

Podemos ver informações como onde ele está localizado , portas abertas e qual é a organização que possui o IP.
Podemos usar a opção **host** seguido do endereço **IP**.
```sh
shodan host 104.18.55.48
```

## Qual o meu IP
Podemos usar a opção **myip** para nos retornar nosso endereço **IP**.
```sh
shodan myip
```

## Analisando numero de alvos (count)
Vamos imaginar o cenario em que temos em mãos um **exploit** ou até o **zero-day** do **Apache 2.4**.

Podemos ter uma ideia de quantos possiveis alvos estaram disponiveis , podemos usar a opção **count**.

```sh
shodan count Apache 2.4
```

Nesse caso foi retornado **70147** hosts usando o **Apache 2.4**.

## Salvando alvos (download)
Podemos criar um arquivo e salvar os alvos para analisar futuros host vulneraveis.

Vamos usar a opção **download**.

Vamos salvar o arquivo como nome de **apache-2.4**.

E vamos pesquisar por hosts usando **Apache 2.4**.
```sh
shodan download apache-2.4 Apache 2.4
```

Podemos ver a saida com **70147** possiveis alvos.
```sh

Search query:			Apache 2.4
Total number of results:	70147
Query credits left:		0
Output file:			apache-2.4.json.gz
  []  100%             
Notice: fewer results were saved than requested
Saved 100 results into file apache-2.4.json.gz
```

Devido a nossa conta ser uma conta **free** vamos ter apenas **100 resultados** salvos em nosso arquivo de saida.

O nosso arquivo de saida é o **apache-2.4.json.gz**.

## Filtrando arquivo usando (parser)
Podemos usar a opção **parser** para filtrar os dados obtidos em nossa pesquisa usando o **download** anteriormente.

Ele nos permite filtrar campos , filtrar o arquivo **JSON** em um **CSV** e é amigavel para usar com outros programas.

O exemplo abaixo filtra o **IP** , **porta** e a **organização**.

Não podemos esquecer que o arquivo **apache-2.4.json.gz** foi criado usado a opção **download**.
```sh
shodan parse --fields ip_str,port,org --separator , apache-2.4.json.gz
```

A saida vai ser algo como
```sh
50.57.241.67,80,Liquid Web, L.L.C,
61.128.111.161,80,CNINFONET Xingjiang,
50.57.255.220,80,Liquid Web, L.L.C,
217.26.52.21,80,Hostpoint AG, Switzerland,
122.144.130.4,80,China Unicom Shanghai network
```

> Ele ter um certo limite para contas free.

## Apenas buscando por alvos (search)
Podemos usar a opção **search** para buscar por alvos.

Por padrão ele vai exibir o **IP**, **Porta** , **nomes de host** e **dados do host**.

Podemos usar a opção **fields** para nos auxiliar a filtrar , no exemplo abaixo vai ser retornado **IP**,**porta**,**organização** e **hostnames** de possiveis alvos usando **Apache 2.4**.
```sh
shodan search --fields ip_str,port,org,hostnames Apache 2.4
```


A saida vai ser algo como
```sh
87.216.162.99   80      Jazz Telecom S.A.       99.162.216.87.static.jazztel.es
2a00:d70:0:b:2002:0:d91a:35a5   80              sl173.web.hostpoint.ch  
50.56.151.158   80      Liquid Web, L.L.C               
184.106.55.63   80      Rackspace Ltd.  lb1-n01.wc1.lan3.stabletransit.com      
217.26.52.127   80      Hostpoint AG, Switzerland       www.airbornescan.com    
159.135.21.159  80      Liquid Web, L.L.C               
77.20.51.99     80      Vodafone Kabel Deutschland      ip4d143363.dynamic.kabel-deutschland.de
202.104.180.155 3749    China Telecom Guangdong province Dongguan MAN netw
```
