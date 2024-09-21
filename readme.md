## Engenharia Reversa Robô NAO v7 

Este projeto visa a colaboração para Engenharia Reversa do Robô NAO v7, parte do Hackathon 
promovido pelo CETEC e a Residência Tecnológica do Porto Digital do Recife com ajuda da EMPREL.
Estudantes de várias instituições privadas do Projeto Embarque Digital foram convidados para um 
Desafio de Integração do Robô NAO, robores empregados no ensino básico municipal há 10 anos, com 
a Inteligência Artificial para auxiliar o desenvolvimento das Escolas da Rede Municipal do Recife.

![NAO Canvas Engenharia Reversa](https://github.com/user-attachments/assets/e7bfa0da-7063-4be5-99bb-86bf1b29bb4f)


## Ideia / Projeto 
1. Explorar o Sistema Operacional do Robô NAO v7.
2. Explorar o interior do NAO com Fotografias e criação de Estratégias de Reparos do Robô.

É uma oportunidade para gerar conhecimentos e aprendizados qualitativos para todos envolvidos que 
surgiu durante o Hackathon para colaborar com a Comunidade Científica e Tecnológica do Porto Digital
bem como as Comunidades: Software Livre, Hardware Livre, Maker, Entusiastas, Empreendedores e Curiosos.

## Vamos em Frente!

Conectar o cabo RJ45 no Robô NAO v7 ao Notebook > Ligar o botão do peito do NAO > Inicia o seu Funcionamento > Sistema Carregado, 
aperta o Botão NAO novamente > Anota o IP do NAO > Usar um Prompt SSH com IP do NAO > Digita Login e Senha > 
Abre o Prompt Shell do NAO Robô

~~~
login as:
Keyboard-interactive authentication prompts from server:
| Password:
End of keyboard-interactive prompts from server
nao7 [0] ~ $ dir
_controle-robo-nao  controle-robo-nao.sh  diagnosis  escutando.wav  naoqi
nao7 [0] ~ $ ls -a
.   .bash_history  .esd_auth        .ipython  .python-history  .trousers
..  .config        .gstreamer-0.10  .local    .rnd             _controle-robo-na
nao7 [0] ~ $
~~~~

Os arquivos que estão com um ponto "." na frente, são arquivos ocultos, e o arquivo  "controle-robo-nao.sh" 
o nome já diz tudo! O Robô NAO é basicamente um LINUX modificado.

Diretórios dentro de /home/nao ~:
~~~
_controle-robo-nao
controle-robo-nao.sh
diagnosis
escutando.wav
naoqi
~~~

Arquivos Ocultos dentro de /home/nao ~:
~~~
.bash_history
.esd_auth
.ipython  
.python-history
.trousers
.config 
.gstreamer-0.10
.local
.rnd  
~~~

## Navegando no NAO v7

Voltaremos a falar dos aquivos e diretórios em /home/nao (~ $) mais na frente.
Mas antes, vamos deixar algumas coisas claras, este tutorial, em princípio, entende que você 
conhece SHELL SCRIPT, pois o ambiente é unicamente Prompt de Comando com Kernel LINUX 2.

Vamos explorar o Sistema Operacional do Robô...

Fiz uma tentativa de salvar tudo de /home/nao/ com o comando "curl", mas o SO retornou um erro
pois o NAO v7 não tem os serviços "sftp" e "scp" para transferência de arquivos pela rede.

~~~

#sftp
nao7 [0] / $ curl -u userNao:senhaNao sftp://169.254.156.177/home/nao/* -o C:\Users\Educação\Documents
                                            [IP DO ROBÔ NAO]
#scp
nao7 [0] / $ curl -u userNao:senhaNao scp://169.254.156.177/home/nao/* -o C:\Users\Educação\Documents
                                           [IP DO ROBÔ NAO]

~~~

O comando "uname -a" detalha o sistema e sua arquitetura. O Nao7 tem uma versão "Linux 4.4.185-rt184-aldebaran x86_64".
Pode ver detalhes da versão "4.4.185-rt184-aldebaran" em nosso repositório LINK.

~~~
nao7 [0] / $ uname -a
Linux nao7 4.4.185-rt184-aldebaran #1 SMP PREEMPT RT Mon Oct 14 14:20:37 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
 
~~~

Listamos as informações de memória com o comando "free -h".

~~~
nao7 [0] / $ free -h
              total        used        free      shared  buff/cache   available
Mem:          3.8Gi       1.2Gi       2.0Gi        13Mi       573Mi       2.5Gi
Swap:            0B          0B          0B
~~~

Listamos as informações de uso do disco com o comando "df -h".

~~~
nao7 [0] / $ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       1.5G  1.4G   35M  98% /
devtmpfs        1.9G     0  1.9G   0% /dev
tmpfs           1.9G  792K  1.9G   1% /dev/shm
tmpfs           250M  8.8M  242M   4% /run
tmpfs           1.9G     0  1.9G   0% /sys/fs/cgroup
tmpfs           1.9G   24K  1.9G   1% /tmp
tmpfs           200M  164K  200M   1% /var/volatile
/dev/mmcblk0p1  120M  8.3M  106M   8% /media/internal
/dev/mmcblk0p4   25G  1.4G   22G   6% /data
overlay          25G  1.4G   22G   6% /var/lib
overlay          25G  1.4G   22G   6% /etc
tmpfs           385M  3.4M  381M   1% /run/user/1001
~~~

Listamos as informações sobre todos os dispositivos de bloco conectados ao sistema "lsblk".
Inclui discos rígidos, SSDs, partições e dispositivos removíveis como pen drives. 

~~~

nao7 [0] / $ lsblk
NAME         MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
mmcblk0      179:0    0 29.1G  0 disk
|-mmcblk0p1  179:1    0  128M  0 part /media/internal
|-mmcblk0p2  179:2    0   64M  0 part
|-mmcblk0p3  179:3    0  3.8G  0 part /
`-mmcblk0p4  179:4    0 25.1G  0 part /data
mmcblk0boot0 179:8    0    4M  1 disk
mmcblk0boot1 179:16   0    4M  1 disk
mmcblk0rpmb  179:24   0    4M  0 disk

~~~

Vejamos quais comandos do Sitema NAO v7 podemos utilizar; o diretório do Linux que guarda todos os comandos 
do sistema é o /bin/bash >...


~~~
nao7 [0] / $ ls
bin  boot  breakpad-syms  data  dev  etc  home  lib  lost+found  media  mnt  nao  opt  proc  root  run  sbin  settings  srv  sys  tmp  usr  var
nao7 [0] / $ cd /bin/bash

~~~



<div style="display: inline_block"><br>
  <img align="center" alt="Igor-Js" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-plain.svg">
  <img align="center" alt="Igor-Ts" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/typescript/typescript-plain.svg">
  <img align="center" alt="Igor-React" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original.svg">
  <img align="center" alt="Igor-HTML" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original.svg">
  <img align="center" alt="Igor-CSS" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original.svg">
  <img align="center" alt="Igor-Python" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg">
  <img align="center" alt="Igor-Csharp" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/csharp/csharp-original.svg">
</div>
  
  ##
 
<div> 
  <a href="" target="_blank"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" target="_blank"></a>
  <a href="https://www.instagram.com/allan_igor_" target="_blank"><img src="https://img.shields.io/badge/-Instagram-%23E4405F?style=for-the-badge&logo=instagram&logoColor=white" target="_blank"></a>
 	<a href="" target="_blank"><img src="https://img.shields.io/badge/Twitch-9146FF?style=for-the-badge&logo=twitch&logoColor=white" target="_blank"></a>
 <a href="" target="_blank"><img src="https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white" target="_blank"></a> 
  <a href = "mailto:studallan@gmail.com"><img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
  <a href="https://www.linkedin.com/in/allan-ribeiro-492b2736" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a> 
  
</div>

