# Linux_do_Zero_Guia_de_Comandos
DIO Linux do Zero: guia de comandos. Aqui estão, resumidamente, todos os comandos do curso e suas utilidades
---

- Comandos essenciais
    - `comando --help` informa o que faz o comando e informa todos os argumentos utilizáveis, junto com suas funções
    x: `ls --help` 
    x: `help cd`
    - `man instrução` retorna o manual de instruções da instrução desejada
    x: `man clear`
    - `hystory` mostra o histórico de comandos (até 1000 comandos)
    - `!!` executa o último comando utilizado
- Navegação
    - `pwd` descubra o diretório em que você está
    - `cd` (change directory) muda o diretório
        - `cd ..` retrocede uma pasta
        - `cd ../pasta` retrocede uma pasta e abre outra desejada
        - `cd /` vai para a raiz principal
        - `cd "expressão"`+ tab (teclado) 
        x: `cd up` +tab. Saída: `cd upstream`
        - `cd "expressão`" + tab x2 (teclado) mostra os diretórios que começam com a expressão citada
        x: `cd up` + tab x2 (teclado). Saída de pastas `/upstream /upword`
    - `ls` lista os arquivos deste diretório
        - `ls “expressão”*` lista os diretórios e seus arquivos que iniciem com a expressão citada 
        x: `ls p*` saída: `pam.d: atd chfn / perl: net`
        Ou seja: traga todos os arquivos e diretório que se iniciem com p e tenham qualquer coisa depois dele.
            
        - `ls “expressão”?”expressão”` lista os diretórios e seus arquivos que iniciem com a expressão citada, que possuem uma outra letra ou número após a expressão, e contenham outra expressão na sequência. 
        x: `ls p*m` saída: `pam.d: atd chfn`
        Ou seja: traga todos os arquivos que se iniciem com p, tenham qualquer número ou letra no segundo index/elemento e tenham m na sequência
- Gerenciar arquivos e pastas
    - CRUD (create, read, update e delete)
        - `touch nomeDoArquivo.formato` cria um arquivo no diretório local 
        x: `touch arquivo.txt`
            - `touch nomeDoArquivo1.formato e nomeDoArquivo2.formato` cria dois arquivos no diretório local, de uma vez
        - `rm nomeDoArquivo.formato` exclui o arquivo desejado
        x: `rm texto.txt`
            - `rm *.txt` exclui todos os arquivos no formato `.txt`
        - `mkdir nomeDaPasta` cria uma pasta no diretório atual
        x: `mkdir pastaExemplo`
            - `mkdir nomeDaPasta1 nomeDaPasta2` cria duas pastas no diretório atual, de uma vez
        - `rmdir nomeDaPasta` excluí a pasta desejada (se estiver vazia)
        x: `rmdir contatos`
            - `rmdir nomeDaPasta1 nomeDaPasta2` excluiu duas pastas de uma vez
            x: `rmdir contatos documentos` (é necessário estar na pasta superior, ou informar o caminho completo das pastas)
        - `rm -rf nomeDodiretório/nomeDaPasta` (recursive forced) exclui todas as subpastas e subarquivos do diretório/pasta informado
        x: `rm -rf documentos` (é necessário estar na pasta superior, ou informar o caminho completo da pasta/diretório)
    - Copiar/Mover/Renomear/Procurar
        - `find -name expressão` procura, a partir do diretório atual, pelo nome do arquivo especificado
        x: `find -name arquivo.txt` ou `find -name arq*`
        - Copiar 1 arquivo:
            - `cp /diretorioArquivo/arquivo.extensão /diretorioDestino`  (cp - copy)
            x: `cp /home/denilson/bancodedados.mdf /disk2/`
        - Copiar vários arquivos que contenham a extensão .txt
            - `cp /diretorioArquivos/*.txt /diretorioDestino`
            x: `cp /home/denilson/*.txt /disk2`
        - Copiar arquivos a partir do diretório em que você está
            - `cp ./arquivo.extensão /diretorioDestino`
        - OBS: Caso você tentar copiar arquivos com o mesmo nome que já estiverem no diretório destino, ele fará a sobreposição. Para evitar isso, utilize a instrução `-i`
        - `-i` instrução indicada para evitar sobreposição, questionando antecipadamente se sobrepõe ou não.
        - `-r` instrução indicada para fazer a cópia recursiva, ou seja, copia-se todas as pastas, arquivos, subpastas e subarquivos presentes no diretório especificado (essencial para backup)
        - `-v` instrução indicada para trazer feedback visual ao usuário, informando os arquivos/pastas que ele está copiando no momento (essencial para caso houver arquivos pesados)
        - Mover 1 arquivo
            - `mv /diretorioArquivo/arquivo.extensão /diretorioDestino`
            x: `mv /home/denilson/planilhas.xlsx /disk2/`
        - OBS: não é possível mover recursivamente, deve-se mover manualmente subpastas e subarquivos
        - Renomear um arquivo
            - `mv nomeDoArquivo.extensão nomeDesejado.extensão`
            x: `mv planilhas.xlsx planilha_investimento.xlsx`
- Gerenciar usuários e grupos
    - Usuário
        - `cat /etc/passwd` mostra a listagem de serviços e usuários
        - `useradd nomeDoUsuario` adiciona um usuário
        `useradd nomeDoUsuario -m` adiciona um usuário e cria seu diretório particular dentro de `/home`
        - `userdel nomeDoUsuario` deleta um usuário
        `userdel nomeDoUsuario -r` deleta um usuário e remove o seu diretório padrão (use -f para forçar)
        - `passwd nomeDoUsuario` define ou redefine a senha para o usuário
        - `usermod nomeDoUsuario -parametro` modifica algum atributo do usuário
        `usermod nomeDoUsuario -s` adiciona cores ao prompt de comando
        `usermod nomeDoUsuario -c "mensagem"` adiciona um comentário específico ao usuário, como sobrenome ou função
        x: `usermod convidado -c "Convidado Especial"`
        - `su nomeDoUsuario` altera o usuário atual para o usuário desejado
        `su maria`
        - `w` como root, lista os usuários, juntamente com IP, horário de login, tempo em espera (idle)
        - `who -a` lista os usuários e seus PIDs (processo de logon)
        - `kill pidUsuario` “derruba” a sessão de um usuário
    - Grupo
        - `cat /etc/group` lista os grupos
        - `usermod -G grupo1, grupo2 nomeDoUsuario` adiciona o usuário aos 2 grupos mencionados, removendo-o de outros grupos anteriores (-G groups, para adicionar apenas a um grupo, use -g e o grupo desejado)
        x: `usermod -G adm, sudo mariana` adiciona a mariana ao grupo adm e sudo, removendo-a aos grupos anteriores
        - `gpasswd -d nomeDoUsuario nomeDoGrupo` remove o usuário do grupo citado (-d delete)
        x: `gpasswd -d mariana adm` remove a mariana do grupo “adm”
- Gerenciar scripts
    - Crie um arquivo executável `nano criar_user.sh`
    - Crie 4 usuários `useradd guest10`
        - Com o comentário “Usuário convidado” `-c “Usuário convidado”`
        - Com o terminal colorido `-s /bin/bash`
        - Com seu diretório particular `-m`
        - Com uma senha padrão `-p $(openss1 passwd -crypt Senha123)`
        - E com expiração de senha no primeiro login `passwd guest10 -e`
    
    ```jsx
    #!/bin/bash
    echo "Criando usuários do sistema...."
    useradd guest10 -c "Usuário convidado" -s /bin/bash -m -p $ (openssl passwd -crypt Senha123)
    passwd guest10 -e
    
    useradd guest11 -c "Usuário convidado" -s /bin/bash -m -p $ (openssl passwd -crypt Senha123)
    passwd guest11 -e
    
    useradd guest12 -c "Usuário convidado" -s /bin/bash -m -p $ (openssl passwd -crypt Senha123)
    passwd guest12 -e
    
    useradd guest13 -c "Usuário convidado" -s /bin/bash -m -p $ (openssl passwd -crypt Senha123)
    passwd guest13 -e
    
    echo "Finalizado!!"
    ```
    
    - `chmod +x  nomeDoArquivo.extensão` concede a permissão de execução do arquivo para o dono
    x: `chmod +x criar_user.sh`
    - `./nomeDoArquivo.extensão` executa o arquivo desejado
    x: `./criar_user.sh`
- Permissões
    - `ls -l` lista todos os arquivos e pastas do diretório atual, incluindo as permissões, tamanho e data de criação
        - Na imagem abaixo tem-se, da esquerda pra direita:
            - Permissões: `lrwxrwxrwx`
               
                ![permissao](https://i.imgur.com/5gVsstl.png)
                
                - A primeira letra informa o que é o arquivo Link `l` (redirecionamento de diretório) Diretório `d` Arquivo `-`
                - os 3 conjuntos de letra são as permissões de leitura `r` escrita `w` e execução`x`.
            - Quantidade de arquivos
            - Dono do arquivo/diretório
            - Grupo pertencente
            - Tamanho em bytes
            - Data e hora criada
            - Nome do Arquivo/Diretório/Links
        
        ![ls-l](https://i.imgur.com/EJV0ntl.png)
        
    - `chown nomeDoUsuario:nomeDoGrupo /nomeDoDiretorio` troca o dono do diretório para o usuário e grupo citados (chown = change owner. Só é possível com sudo ou root)
    x: `chown debora:GRP_ADM /adm/`
    - `chown nomeDoUsuario:nomeDoGrupo arquivo.extensão` troca o dono do grupo para o usuário e grupo citados
    x: `chown root:GRP_ADM texto-adm.txt`
    - Nível de permissões: conforme a tabela abaixo, se você quer ter privilégio de Leitura (R) e Gravação (W), terá que informar o valor 6. Se quiser ter R W e X, valor 7. Apenas X? 1. W e X? 3. Nenhuma? 0.
        
        ![tabela](https://i.imgur.com/Y4nz6ry.png)
        
    - Sigla `ndp`: nível de permissão (para ficar mais curto o código abaixo)
    - `chmod **ndpROOTndpGROUPndpOTHER** /diretorio` concede privilégios específicos para o root, grupo e outros para um diretório específico
    `chmod 775 /adm` dá permissão RWX ao root, RWX ao grupo e RX aos outros
    - `chmod **ndpROOTndpGROUPndpOTHER** /arquivo.extensão` concede privilégios específicos para o root, grupo e outros para um arquivo específico
    x: `chmod 750 texto-adm.txt`
    - `chmod +x  nomeDoArquivo.extensão` concede a permissão de execução do arquivo para o dono
    x: `chmod +x criar_user.sh`
    - `chmod -x  nomeDoArquivo.extensão` remove a permissão de execução do arquivo para o dono
    x: `chmod -x criar_user.sh`
- Gerenciar pacotes
    - `apt list installed` lista os aplicativos instalados na máquina
    - `apt list --upgradable` lista os aplicativos instalados que possuem atualização disponível
    - `apt search nomeDoAplicativo` procura aplicativos nos repositórios do ubuntu com o nome citado
    - `apt install nomeDoAplicativo` instala um aplicativo
    x: `apt install net-tools`
    - `apt-get install nomeDoAplicativo` instala um aplicativo
    - `apt-get update nomeDoAplicativo`  faz o download da atualização de um aplicativo
    - `apt-get upgrade nomeDoAplicativo` executa a atualização de um aplicativo
    - `wget link` baixa o(s) arquivo(s) deste link para o diretório atual
    x: `wget [https://github.com/BrunoThums/Web-Scraping-Practice/archive/refs/heads/main.zip](https://github.com/BrunoThums/Web-Scraping-Practice/archive/refs/heads/main.zip)` baixa para o diretório atual
    - `apt remove nomeDoPrograma` remove um aplicativo
    x: `apt remove net-tools`
    - `apt update` faz o download da atualização dos pacotes do sistema
    - `apt upgrade` faz a instalação das atualizações dos pacotes do sistema
    - 
- Gerenciar discos
    - Particionar o disco
        - Escolha o disco desejado ( ex: `/dev/sdb` )
        - `fdisk caminhoDoDisco` abre o fdisk para o disco escolhido
        x: `fdisk /dev/sdb`
        - `n` cria uma nova partição
        - `p` para primária `e` para extendida
        - `1` numero da partição (de 1 a 4, se for a primeira, escolha `1`)
        - ***************`pressiona enter`* entra com a quantidade de bytes do primeiro setor (*****enter***** para o padrão)
        - ***************`pressiona enter`* entra com a quantidade de bytes do último setor (*****enter***** para o padrão). Utiliza todo o disco para esta “partição”
        - `w` salva as alterações
        - `mkfs.formato /diretorioDoDisco` formata o disco para o formato Ext4
        x: `mkfs.ext4 /dev/sdb`
        - `y` para confirmar a formatação
    - Sistema de arquivos linux: `Ext3`, `Ext4`, `XFS`
    - No Windows temos os discos C: D: E:
    - No Linux, cada disco inicia por **sd** (disco físico)e termina com uma numeração (correspondendo às suas partições):
        - x: **sd**a1, **sd**a2, **sd**b1. (sda corresponde ao disco rígido Adata, por exemplo, e os números 1 e 2 são suas partições)
    - Adicionar um disco rígido
    - `lsblk` lista os discos disponíveis no computador, informando onde estão montados, juntamente com o local das partições.
    - `fdisk -l` lista os discos disponíveis no computador com mais detalhes (-l = list)
    - `mount /diretorioDoDisco /nomeDaPastaExistente (vazia)` monta o disco nesta pasta (significa que o conteúdo do disco passa a existir dentro desta pasta
    `mount /dev/sdb /disk2` (lembre-se de fazer o próximo comando para efetivar essas alterações, pois do contrário elas se perdem ao reiniciar a máquina, terá sempre que fazer o `mount`)
    - `nano /etc/fstab` e adicione uma linha ao final com:
    `nomeDodisco + localMontado + formatoDoSistemaDeArquivos + parâmetrosPadrões`
    x: `/dev/sdb /disk2 etx4 defaults 0 0` salve com CTRL+O Enter CTRL+X
    - Faça o reboot para confirmar as modificações
- Gerenciar processos
    - `ps` lista os processos do usuário atual
        - `-a` parâmetro indicado para mostrar os processos de todos os usuários
        - `-u` parâmetro indicado para exibir o nome do usuário e horário de início do processo
        - `-x` parâmetro indicado para exibir processos executados fora do console
    - `kill pidDoProcesso` elimina o processo com base no código PID
    x: `kill 12852`
    - `killall nomeDoAplicativo` elimina todos os processos de um determinado processo
    x: `killall chrome`
- Desafio: Infraestrutura como Código (IaC)
    
    ![Desafio](https://i.imgur.com/LW7wzVx.png)
    
    - Todo provisionamento deve ser feito em um arquivo do tipo Bash Script;
        - `nano script.sh`
    - Excluir diretórios, grupos e usuários criados anteriormente:
        - `rm -Rf /adm`
        - `groupdel GRP_ADM`
        - `userdel -r maisa`
    - Criar usuários e atribuí-los aos grupos
        - `useradd carlos -m -g GRP_ADM -p $ (openssl passwd -crypt Senha123)`
        `passwd carlos -e`
    - Os usuários de cada grupo terão permissão total dentro de seu respectivo diretório;
    - Os usuários não poderão ter permissão de leitura, escrita e execução em diretórios de departamentos que eles não pertencem;
    - Criar as pastas e definir as permissões (root 7, grupo 7, outros 0)
        - `mkdir /adm -m 770`
        - `mkdir /ven -m 770`
        - `mkdir /sec -m 770`
        - `mkdir /public -m 777`
    - Cria os grupos
        - `groupadd GRP_ADM`
        - `groupadd GRP_VEN`
        - `groupadd GRP_SEC`
    - O dono de todos os diretórios criados será o usuário root;
        - `chown root:GRP_ADM /adm`
        - `chown root:GRP_ADM /ven`
        - `chown root:GRP_ADM /sec`
    - Todos os usuários terão permissão total dentro do diretório publico;
        - `chmod 777 /publico`
    - Subir arquivo de script criado para a sua conta no GitHub.
    - `nano start_environment_pattern.sh`
    
    ```bash
    #!/bin/bash
    
    echo "Deletando pastas dos usuários..."
    
    rm -Rf /adm/
    #defina outras pastas aqui
    
    echo "Pastas deletadas!"
    
    echo "Excluindo usuários do sistema..."
    
    userdel -r maisa
    #defina outros usuários aqui
    
    echo "Usuários excluídos!"
    
    echo "Criando os diretórios com suas permissões..."
    
    mkdir /adm -m 770
    mkdir /ven -m 770
    mkdir /sec -m 770
    mkdir /publico -m 777
    
    echo "Diretórios criados!"
    
    echo "Criando os Grupos..."
    
    groupadd GRP_ADM
    groupadd GRP_VEN
    groupadd GRP_SEC
    
    echo "Grupos criados!"
    
    echo "Criando usuários do sistema e separando em seus grupos..."
    #GRUPO GRP_ADM
    #cria o usuário carlos
    useradd carlos -m -g GRP_ADM -p $ (openssl passwd -crypt Senha123)
    passwd carlos -e
    
    #cria o usuário maria
    useradd maria -m -g GRP_ADM -p $ (openssl passwd -crypt Senha123)
    passwd maria -e
    
    #cria o usuário joão
    useradd joao -m -g GRP_ADM -p $ (openssl passwd -crypt Senha123)
    passwd joao -e
    
    #GRUPO GRP_VEN
    #cria o usuário debora
    useradd debora -m -g GRP_VEN -p $ (openssl passwd -crypt Senha123)
    passwd debora -e
    
    #cria o usuário sebastiano
    useradd sebastiano -m -g GRP_VEN -p $ (openssl passwd -crypt Senha123)
    passwd sebastiano -e
    
    #cria o usuário roberto
    useradd roberto -m -g GRP_VEN -p $ (openssl passwd -crypt Senha123)
    passwd roberto -e
    
    #GRUPO GRP_SEC
    #cria o usuário josefina
    useradd josefina -m -g GRP_SEC -p $ (openssl passwd -crypt Senha123)
    passwd josefina -e
    
    #cria o usuário amanda
    useradd amanda -m -g GRP_SEC -p $ (openssl passwd -crypt Senha123)
    passwd amanda -e
    
    #cria o usuário rogerio
    useradd rogerio -m -g GRP_SEC -p $ (openssl passwd -crypt Senha123)
    passwd rogerio -e
    
    echo "Usuários criados!"
    
    echo "Definindo o root como dono dos diretórios..."
    
    chown root:GRP_ADM /adm
    chown root:GRP_ADM /ven
    chown root:GRP_ADM /sec
    
    echo "Root agora é dono dos diretórios!"
    
    echo "Script executado com sucesso!"
    ```
    
    - `chmod +x  start_environment_pattern.sh`concede a permissão de execução do arquivo
    - `./start_environment_pattern.sh` executa o arquivo desejado
    

- Servidores
    - São utilizados como: servidor de arquivos, servidor web e servidor de banco de dados.
    - Servidor de arquivos
        - É necessário instalar o samba (para manipular arquivos SMB, do Windows)
        `apt install samba -y`
        - Cria-se uma pasta publica
        `mkdir publica`
        - Com permissão total a todos
        `chmod 777 publica`
        - Abre-se o arquivo de configuração do samba
        `nano /etc/samba/smb.conf`
        - Vá até o final do arquivo e adicione as seguintes linhas
        
        ```bash
        #[nomeDaPastaPublica/PastaParaSeCompartilhar]
        [publica]
        #path = diretórioDaPasta
        path = /disk2/publica
        writable = yes
        #Definir para que qualquer pessoa tenha acesso à pasta
        guest ok = yes
        #Definir que todos que acessarem serão apenas convidados (guest)
        guest only = yes
        #CTRL+O enter CTRL+X
        ```
        
        - O `systemctl` gerencia serviços em segundo plano. Neste caso vamos reiniciar o `smb` (samba). Termina em “d” pois ele é um `daemon` (serviço em segundo plano)
        `systemctl restart` 
        `systemctl restart smbd`
        - Verifique se o processo está em execução
        `systemctl status smbd`
        - Para iniciar o processo, use
        `systemctl enable smbd`
        - Verifique o ip do samba
        `ip a`
        - Para acessar o samba pelo Windows, abra o explorador de arquivos, e onde mostra o diretório, digite o ip
        `\\10.0.0.19\publica` e enter
        - OBS: só é possível acessar a pasta as pessoas cadastradas na lista do servidor
        `cat /etc/passwd`
        - É possível acessar conectando-se a um local de rede
            
            ![mapear unidade de rede](https://i.imgur.com/Xk3opkT.png)
            
    - Servidor Web
        - Instale o apache2
        `apt install apache2 -y`
        - Verifique se ele já está em execução
        `systemctl status apache2`
        - Verifique o ip do apache
        `ip a`
        - Abra o Chrome e conecte-se ao IP
        - Altere o conteúdo do index.html ou o exclua. Ele está no diretório
        `cd /var/www/html`
        - Para remover use
        `rm index.html`
        - E crie um novo
        `nano index.html`
        - Este servidor estará apenas habilitado localmente (apenas na sua rede). Para disponibilizar mundialmente, é necessário conectar por meio de um servidor (AWS, por exemplo)
- Desafio: Infraestrutura como Código (IaC)
    - Restaurar o snapshot criado anteriormente no virtualbox;
    - Atualizar o servidor;
    - Instalar o apache2;
    - Instalar o unzip;
    - Baixar a aplicação disponível no endereço
    - [https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip](https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip) no diretório /tmp;
    - Copiar os arquivos da aplicação no diretório padrão do apache;
    - Subir arquivo de script para um repositório no GitHub.
    - `nano start_apache_environment.sh`
    
    ```bash
    #!/bin/bash
    echo "Atualizando o servidor..."
    apt-get update -y
    echo "Instalando as atualizações..."
    apt-get upgrade -y
    echo "Instalando apache2..."
    apt install apache2 -y
    echo "Instalando unzip..."
    apt install unzip -y
    echo "Baixando linux-site-dio do github"
    wget -P /tmp [https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/main.zip](https://github.com/denilsonbonatti/linux-site-dio/archive/refs/heads/mai)
    echo "Deszipando o conteúdo"
    unzip main.zip
    echo "Copiando para o ambiente do apache"
    cp -R * /tmp/linux-site-dio-main /var/www/html
    ```
    
- `chmod +x  start_environment_pattern.sh`concede a permissão de execução do arquivo
- `./start_environment_pattern.sh` executa o arquivo desejado
