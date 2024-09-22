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

Fiz uma tentativa de salvar tudo de /home/nao/ com o comando "curl", mas o CMD WINDOWS retornou um erro
pois o Sistena Operacional - SO do NAO v7 não tem os serviços "sftp" e "scp" para transferência de arquivos pela rede.

~~~

#sftp
CMD WINDOWS11 $ curl -u userNao:senhaNao sftp://169.254.156.177/home/nao/* -o C:\Users\Educação\Documents
                                            [IP DO ROBÔ NAO]
#scp
CMD WINDOWS11 $ curl -u userNao:senhaNao scp://169.254.156.177/home/nao/* -o C:\Users\Educação\Documents
                                           [IP DO ROBÔ NAO]

~~~

O comando "uname -a" detalha o sistema e sua arquitetura. O Nao7 tem uma versão "Linux 4.4.185-rt184-aldebaran x86_64 GNU/LINUX".
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

Listamos as informações sobre todos os dispositivos de bloco conectados ao sistema com o comando "lsblk".
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

Vejamos quais comandos do Sitema NAO v7 podemos utilizar! O diretório do Linux que guarda todos os comandos 
do sistema é o /bin com o comando "ls -l -a" que combina duas opções do comando "ls" para listar arquivos e diretórios com mais detalhes e incluir arquivos ocultos.


<details>
  <summary>..........>>CLIQUE PARA EXPANDIR O CÓDIGO<<............</summary>

  ```

nao7 [0] / $ ls
bin  boot  breakpad-syms  data  dev  etc  home  lib  lost+found  media  mnt  nao  opt  proc  root  run  sbin  settings  srv  sys  tmp  usr  var
nao7 [0] / $ cd /bin
nao7 [0] /bin $ ls -l -a
total 7080
drwxr-xr-x  2 root root    4096 Oct 14  2019 .
drwxr-xr-x 24 root root    4096 Aug 20  2021 ..
-rwxr-xr-x  1 root root   25992 Oct 14  2019 arping
lrwxrwxrwx  1 root root      25 Oct 14  2019 base64 -> /usr/bin/base64.coreutils
lrwxrwxrwx  1 root root      14 Oct 14  2019 bash -> /bin/bash.bash
-rwxr-xr-x  1 root root 1243444 Oct 14  2019 bash.bash
lrwxrwxrwx  1 root root      18 Oct 14  2019 cat -> /bin/cat.coreutils
-rwxr-xr-x  1 root root   46592 Oct 14  2019 cat.coreutils
lrwxrwxrwx  1 root root      21 Oct 14  2019 chattr -> /bin/chattr.e2fsprogs
-rwxr-xr-x  1 root root   13648 Oct 14  2019 chattr.e2fsprogs
lrwxrwxrwx  1 root root      20 Oct 14  2019 chgrp -> /bin/chgrp.coreutils
-rwxr-xr-x  1 root root   87520 Oct 14  2019 chgrp.coreutils
lrwxrwxrwx  1 root root      20 Oct 14  2019 chmod -> /bin/chmod.coreutils
-rwxr-xr-x  1 root root   71136 Oct 14  2019 chmod.coreutils
lrwxrwxrwx  1 root root      20 Oct 14  2019 chown -> /bin/chown.coreutils
-rwxr-xr-x  1 root root   87520 Oct 14  2019 chown.coreutils
-rwsr-xr-x  1 root root   17736 Oct 14  2019 clockdiff
lrwxrwxrwx  1 root root      17 Oct 14  2019 cp -> /bin/cp.coreutils
-rwxr-xr-x  1 root root  140768 Oct 14  2019 cp.coreutils
lrwxrwxrwx  1 root root      19 Oct 14  2019 date -> /bin/date.coreutils
-rwxr-xr-x  1 root root  132576 Oct 14  2019 date.coreutils
lrwxrwxrwx  1 root root      17 Oct 14  2019 dd -> /bin/dd.coreutils
-rwxr-xr-x  1 root root   99844 Oct 14  2019 dd.coreutils
lrwxrwxrwx  1 root root      21 Oct 14  2019 df -> /usr/bin/df.coreutils
lrwxrwxrwx  1 root root      21 Oct 14  2019 dmesg -> /bin/dmesg.util-linux
-rwxr-xr-x  1 root root   79384 Oct 14  2019 dmesg.util-linux
lrwxrwxrwx  1 root root      19 Oct 14  2019 echo -> /bin/echo.coreutils
-rwxr-xr-x  1 root root   34260 Oct 14  2019 echo.coreutils
lrwxrwxrwx  1 root root      15 Oct 14  2019 egrep -> /bin/egrep.grep
-rwxr-xr-x  1 root root      28 Oct 14  2019 egrep.grep
lrwxrwxrwx  1 root root      20 Oct 14  2019 false -> /bin/false.coreutils
-rwxr-xr-x  1 root root   34260 Oct 14  2019 false.coreutils
lrwxrwxrwx  1 root root      15 Oct 14  2019 fgrep -> /bin/fgrep.grep
-rwxr-xr-x  1 root root      28 Oct 14  2019 fgrep.grep
lrwxrwxrwx  1 root root      22 Oct 14  2019 getopt -> /bin/getopt.util-linux
-rwxr-xr-x  1 root root   17792 Oct 14  2019 getopt.util-linux
lrwxrwxrwx  1 root root      14 Oct 14  2019 grep -> /bin/grep.grep
-rwxr-xr-x  1 root root  271904 Oct 14  2019 grep.grep
lrwxrwxrwx  1 root root       3 Oct 14  2019 gtar -> tar
lrwxrwxrwx  1 root root      16 Oct 14  2019 gunzip -> /bin/gunzip.gzip
-rwxr-xr-x  2 root root    2345 Oct 14  2019 gunzip.gzip
lrwxrwxrwx  1 root root      14 Oct 14  2019 gzip -> /bin/gzip.gzip
-rwxr-xr-x  1 root root  108752 Oct 14  2019 gzip.gzip
lrwxrwxrwx  1 root root      23 Oct 14  2019 hostname -> /bin/hostname.inetutils
-rwxr-xr-x  1 root root   38372 Oct 14  2019 hostname.coreutils
-rwxr-xr-x  1 root root   55028 Oct 14  2019 hostname.inetutils
-rwxr-xr-x  1 root root   62848 Oct 14  2019 journalctl
lrwxrwxrwx  1 root root      16 Oct 14  2019 kill -> /bin/kill.procps
-rwxr-xr-x  1 root root   42904 Oct 14  2019 kill.coreutils
-rwxr-xr-x  1 root root   25980 Oct 14  2019 kill.procps
-rwxr-xr-x  1 root root   38272 Oct 14  2019 kill.util-linux
-rwxr-xr-x  1 root root  169384 Oct 14  2019 kmod
lrwxrwxrwx  1 root root      17 Oct 14  2019 ln -> /bin/ln.coreutils
-rwxr-xr-x  1 root root   83428 Oct 14  2019 ln.coreutils
lrwxrwxrwx  1 root root      17 Oct 14  2019 login -> /bin/login.shadow
-rwxr-xr-x  1 root root   51296 Oct 14  2019 login.shadow
-rwxr-xr-x  1 root root   54660 Oct 14  2019 loginctl
lrwxrwxrwx  1 root root      17 Oct 14  2019 ls -> /bin/ls.coreutils
-rwxr-xr-x  1 root root  173796 Oct 14  2019 ls.coreutils
-rwxr-xr-x  1 root root   14623 Oct 14  2019 lsb_release
lrwxrwxrwx  1 root root      15 Oct 14  2019 lsmod -> /bin/lsmod.kmod
lrwxrwxrwx  1 root root       4 Oct 14  2019 lsmod.kmod -> kmod
-rwxr-xr-x  1 root root   83340 Oct 14  2019 machinectl
lrwxrwxrwx  1 root root      20 Oct 14  2019 mkdir -> /bin/mkdir.coreutils
-rwxr-xr-x  1 root root   58848 Oct 14  2019 mkdir.coreutils
lrwxrwxrwx  1 root root      20 Oct 14  2019 mknod -> /bin/mknod.coreutils
-rwxr-xr-x  1 root root   46560 Oct 14  2019 mknod.coreutils
lrwxrwxrwx  1 root root      25 Oct 14  2019 mktemp -> /usr/bin/mktemp.coreutils
lrwxrwxrwx  1 root root      20 Oct 14  2019 more -> /bin/more.util-linux
-rwxr-xr-x  1 root root   42356 Oct 14  2019 more.util-linux
lrwxrwxrwx  1 root root      21 Oct 14  2019 mount -> /bin/mount.util-linux
-rwsr-xr-x  1 root root   42372 Oct 14  2019 mount.util-linux
lrwxrwxrwx  1 root root      26 Oct 14  2019 mountpoint -> /bin/mountpoint.util-linux
-rwxr-xr-x  1 root root   13700 Oct 14  2019 mountpoint.util-linux
lrwxrwxrwx  1 root root      17 Oct 14  2019 mv -> /bin/mv.coreutils
-rwxr-xr-x  1 root root  157156 Oct 14  2019 mv.coreutils
lrwxrwxrwx  1 root root      23 Oct 14  2019 nice -> /usr/bin/nice.coreutils
lrwxrwxrwx  1 root root      17 Oct 14  2019 pidof -> /bin/pidof.procps
-rwxr-xr-x  1 root root   17788 Oct 14  2019 pidof.procps
lrwxrwxrwx  1 root root      17 Oct 14  2019 ping -> /bin/ping.iputils
-rwsr-xr-x  1 root root   71632 Oct 14  2019 ping.iputils
lrwxrwxrwx  1 root root      27 Oct 14  2019 printenv -> /usr/bin/printenv.coreutils
lrwxrwxrwx  1 root root      14 Oct 14  2019 ps -> /bin/ps.procps
-rwxr-xr-x  1 root root  120356 Oct 14  2019 ps.procps
lrwxrwxrwx  1 root root      18 Oct 14  2019 pwd -> /bin/pwd.coreutils
-rwxr-xr-x  1 root root   46560 Oct 14  2019 pwd.coreutils
-rwxr-xr-x  1 root root   17836 Oct 14  2019 rarpd
-rwxr-xr-x  1 root root   25984 Oct 14  2019 rdisc
lrwxrwxrwx  1 root root      17 Oct 14  2019 rm -> /bin/rm.coreutils
-rwxr-xr-x  1 root root   83424 Oct 14  2019 rm.coreutils
lrwxrwxrwx  1 root root      20 Oct 14  2019 rmdir -> /bin/rmdir.coreutils
-rwxr-xr-x  1 root root   54752 Oct 14  2019 rmdir.coreutils
lrwxrwxrwx  1 root root      12 Oct 14  2019 sed -> /bin/sed.sed
-rwxr-xr-x  1 root root  161628 Oct 14  2019 sed.sed
lrwxrwxrwx  1 root root      14 Oct 14  2019 sh -> /bin/bash.bash
lrwxrwxrwx  1 root root      20 Oct 14  2019 sleep -> /bin/sleep.coreutils
-rwxr-xr-x  1 root root   38368 Oct 14  2019 sleep.coreutils
lrwxrwxrwx  1 root root      19 Oct 14  2019 stat -> /bin/stat.coreutils
-rwxr-xr-x  1 root root  108000 Oct 14  2019 stat.coreutils
lrwxrwxrwx  1 root root      19 Oct 14  2019 stty -> /bin/stty.coreutils
-rwxr-xr-x  1 root root   91616 Oct 14  2019 stty.coreutils
lrwxrwxrwx  1 root root      14 Oct 14  2019 su -> /bin/su.shadow
-rwsr-xr-x  1 root root   43228 Oct 14  2019 su.shadow
-rwsr-xr-x  1 root root   50556 Oct 14  2019 su.util-linux
lrwxrwxrwx  1 root root      19 Oct 14  2019 sync -> /bin/sync.coreutils
-rwxr-xr-x  1 root root   38368 Oct 14  2019 sync.coreutils
-rwxr-xr-x  1 root root  198016 Oct 14  2019 systemctl
-rwxr-xr-x  1 root root   13708 Oct 14  2019 systemd-ask-password
-rwxr-xr-x  1 root root   13688 Oct 14  2019 systemd-escape
-rwxr-xr-x  1 root root   34172 Oct 14  2019 systemd-firstboot
-rwxr-xr-x  1 root root  128648 Oct 14  2019 systemd-hwdb
-rwxr-xr-x  1 root root   13696 Oct 14  2019 systemd-inhibit
-rwxr-xr-x  1 root root   17796 Oct 14  2019 systemd-machine-id-setup
-rwxr-xr-x  1 root root   13696 Oct 14  2019 systemd-notify
-rwxr-xr-x  1 root root   46464 Oct 14  2019 systemd-sysusers
-rwxr-xr-x  1 root root   75136 Oct 14  2019 systemd-tmpfiles
-rwxr-xr-x  1 root root   30092 Oct 14  2019 systemd-tty-ask-password-agent
lrwxrwxrwx  1 root root      12 Oct 14  2019 tar -> /bin/tar.tar
-rwxr-xr-x  1 root root  605664 Oct 14  2019 tar.tar
-rwxr-xr-x  1 root root   17912 Oct 14  2019 tftpd
lrwxrwxrwx  1 root root      20 Oct 14  2019 touch -> /bin/touch.coreutils
-rwxr-xr-x  1 root root  120288 Oct 14  2019 touch.coreutils
-rwxr-xr-x  1 root root   17744 Oct 14  2019 tracepath
-rwsr-xr-x  1 root root   17752 Oct 14  2019 traceroute6
lrwxrwxrwx  1 root root      19 Oct 14  2019 true -> /bin/true.coreutils
-rwxr-xr-x  1 root root   34260 Oct 14  2019 true.coreutils
-rwxr-xr-x  2 root root  673436 Oct 14  2019 udevadm
lrwxrwxrwx  1 root root      22 Oct 14  2019 umount -> /bin/umount.util-linux
-rwsr-xr-x  1 root root   30080 Oct 14  2019 umount.util-linux
lrwxrwxrwx  1 root root      20 Oct 14  2019 uname -> /bin/uname.coreutils
-rwxr-xr-x  1 root root   42464 Oct 14  2019 uname.coreutils
-rwxr-xr-x  2 root root    2345 Oct 14  2019 uncompress
lrwxrwxrwx  1 root root      17 Oct 14  2019 vi -> /usr/bin/vim.tiny
lrwxrwxrwx  1 root root      17 Oct 14  2019 watch -> /bin/watch.procps
-rwxr-xr-x  1 root root   22048 Oct 14  2019 watch.procps
lrwxrwxrwx  1 root root      14 Oct 14  2019 zcat -> /bin/zcat.gzip
-rwxr-xr-x  1 root root    1983 Oct 14  2019 zcat.gzip

```
</details>

```
# Pré-apresentação do diretório /bin clique em ">>CLIQUE PARA EXPANDIR O CÓDIGO<<" para ver completo!
nao7 [0] / $ ls
bin  boot  breakpad-syms  data  dev  etc  home  lib  lost+found  media  mnt  nao  opt  proc  root  run  sbin  settings  srv  sys  tmp  usr  var
nao7 [0] / $ cd /bin
nao7 [0] /bin $ ls -l -a
total 7080
drwxr-xr-x  2 root root    4096 Oct 14  2019 .
drwxr-xr-x 24 root root    4096 Aug 20  2021 ..
-rwxr-xr-x  1 root root   25992 Oct 14  2019 arping
lrwxrwxrwx  1 root root      25 Oct 14  2019 base64 -> /usr/bin/base64.coreutils
lrwxrwxrwx  1 root root      14 Oct 14  2019 bash -> /bin/bash.bash
-rwxr-xr-x  1 root root 1243444 Oct 14  2019 bash.bash
lrwxrwxrwx  1 root root      18 Oct 14  2019 cat -> /bin/cat.coreutils
-rwxr-xr-x  1 root root   46592 Oct 14  2019 cat.coreutils
lrwxrwxrwx  1 root root      21 Oct 14  2019 chattr -> /bin/chattr.e2fsprogs
-rwxr-xr-x  1 root root   13648 Oct 14  2019 chattr.e2fsprogs
lrwxrwxrwx  1 root root      20 Oct 14  2019 chgrp -> /bin/chgrp.coreutils
-rwxr-xr-x  1 root root   87520 Oct 14  2019 chgrp.coreutils..........................................................
```

Não é nosso propósito explicar cada comando, executável e interpretador contidos no diretório /bin, faremos isso mais na frente 
separando os que são puro LINUX para focar nos que foram incluídos pelo fabricante. Uma breve explicação dos motivos de 
listar os arquivos deste diretório: Tentei obter informações de hardware do NAO v7 como comando "lshw", mas o "bash", 
que é o interpretador do Shell retornou um erro. Por enquanto só podemos trabalhar com os comandos que o NAO v7 pode suportar. 

Continue-mos nossa exploração...

## Bate o Coração do Robô NAO v7 

Com o comando "top" verifiquei os processos em execução detalhados do Sistema Operacional enquanto o Robô estava "Parado" e "Movimentando".
Foi bem interessante esta exploração, foi como ver o seu coração bater! Do lado esquerdo do vídeo o Robô NAO v7 esta "parado", e do lado direito do vídeo o Robô NAO v7 está execultando
uma performance de "Alongamento Academia" iniciado pelo programa "Choreographe", com som e movimentos dos braços e sensores. Vejam a seguir o robô parado: 

````
# Robô NAO v7 PARADO
nao7 [0] / $ top
````
![TOP PARADO NAO V7](https://github.com/user-attachments/assets/00115364-d42b-4e51-865e-a9362e9bc5cb)


## Comandos "cat" e "vi"

Como listamos em /bin o Robô NAO v7 aceita o editor de arquivos comando "vi" do Linux e o Leitor de arquivos comando "cat".
Vamos fazer uma varredura nos arquivos de /home/nao para entender quais suas funções no funcionamento do Robô NAO v7.

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

