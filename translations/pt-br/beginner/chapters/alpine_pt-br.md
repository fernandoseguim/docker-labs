## 1.0 Rodando o seu primeiro contêiner

Agora que você está com o Docker configurado, é hora de colocar a mão na massa. Nesta seção, você irá rodar um contêiner do [Alpine Linux](http://www.alpinelinux.org/) (uma leve distribuição linux) en seu sistema e praticar o comando `docker run`.

Para começar, vamos executar o seguinte comando no terminal:

```
$ docker pull alpine
```

> **Nota:** Dependendo de como você tem o docker em seu sistema, você pode ter o erro `permission denied` após executar o comando acima. Tente os comandos de do tutorial de introdução para [verificar sua instalação](https://docs.docker.com/engine/getstarted/step_one/#/step-3-verify-your-installation). Se você está usando o Linux, talvez você acrescentar o prefixo `sudo` antes do comando `docker`. Como alternativa, você pode [criar um grupo](https://docs.docker.com/engine/installation/linux/ubuntulinux/#/create-a-docker-group) para solucionar este "problema".

O comando `pull` busca a **imagem** do alpine linux no **Docker registry** e salve em seu sistema. Você pode usar o comando `docker images` para obter a lista de todas as imagens em seu sistema.

```
$ docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
alpine                 latest              c51f86c28340        4 weeks ago         1.109 MB
hello-world             latest              690ed74de00f        5 months ago        960 B
```

### 1.1 Executando o Docker
Perfeito! Agora vamos executar um **contêiner** Docker baseado nesta imagem. Para isto você deve usar o comando `docker run`

```
$ docker run alpine ls -l
total 48
drwxr-xr-x    2 root     root          4096 Mar  2 16:20 bin
drwxr-xr-x    5 root     root           360 Mar 18 09:47 dev
drwxr-xr-x   13 root     root          4096 Mar 18 09:47 etc
drwxr-xr-x    2 root     root          4096 Mar  2 16:20 home
drwxr-xr-x    5 root     root          4096 Mar  2 16:20 lib
......
......
```

O que aconteceu? Por trás dos panos, muitas coisas aconteceram. Quando você executou o comando `run`, o cliente Docker procurou a imagem (neste caso, a do alpine linux), criou o contêiner e em seguida, executou um comando neste contêiner. QUando você executou `docker run alpine`, você acrescentou o comando (`ls -l`), então o Docker iniciou o comando especificado e você viu a listagem.

Vamos tentar algo mais emocionante.

```
$ docker run alpine echo "hello from alpine"
hello from alpine
```

OK, está é apenas uma saída (output). Neste caso, o cliente Docker executou o comando `echo` em nosso contêiner alpine linux e em seguida, saiu dele.

Agora tente outro comando.

```
$ docker run alpine /bin/sh
```

Espere, não aconteceu nada! Será que é um bug? Bem, não é um bug. Shells interativos sairão depois de executar qualquer comandos com script, a menos que eles 


Espere, não aconteceu nada! Será que é um bug? Bem, não é um bug. Estes shells interativos encerrarão após executar qualquer comando, a menos que sejam executados em um terminal interativo - então neste caso, você precisa acrescentar o parâmentro `-it` para rodar o comando `docker run -it alpine /bin/sh`.

Agora você está dentro do contêiner e você pode testar alguns comandos como s `ls -l`, `uname -a`, entre outros. Para sair do contêiner bastar executar o comando `exit`.


OK, agora iremos ver o comando `docker ps`. Este comando exibirá todos os contêiners que estão em execução atualmente.

```
$ docker ps
contêiner ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

Como não há contêiners em execução, você verá uma lista vazia, Agora tente o comando `docker ps -a`.

```
$ docker ps -a
contêiner ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
36171a5da744        alpine              "/bin/sh"                5 minutes ago       Exited (0) 2 minutes ago                        fervent_newton
a6a9d46d0b2f        alpine             "echo 'hello from alp"    6 minutes ago       Exited (0) 6 minutes ago                        lonely_kilby
ff0a5c3750b9        alpine             "ls -l"                   8 minutes ago       Exited (0) 8 minutes ago                        elated_ramanujan
c317d0a9e3d2        hello-world         "/hello"                 34 seconds ago      Exited (0) 12 minutes ago                       stupefied_mcclintock
```

O que você vê acima é uma lista com todos os contêiners que você executou. Observe que a coluna `STATUS` mostra que a execução destes contêiners foram encerradas minutos atrás. Você provavelmente deve estar se perguntando se há uma maneira de executar mais de um comando em um contêiner. Vamos tentar isso agora:

```
$ docker run -it alpine /bin/sh
/ # ls
bin      dev      etc      home     lib      linuxrc  media    mnt      proc     root     run      sbin     sys      tmp      usr      var
/ # uname -a
Linux 97916e8cb5dc 4.4.27-moby #1 SMP Wed Oct 26 14:01:48 UTC 2016 x86_64 Linux
```

Executando o comando `run` com o parâmetro `-it` nos retornará um terminal interativo no contêiner. Agora você poderá executar diversos comandos no contêiner como desejar. Teste com alguns dos seus comandos favoritos do linux.

Isso conclui a excusão em torno do comando `docker run` que provavelmente será o comando que você mais irá utilizar. Passe mais algum tempo  praticando-o. Para saber mais sobre o comando `run`, use o comando `docker run --help` para ver um lista com todos os parâmetros suportados. A medida que evoluirmos neste tutorial, veremos mais algumas aplicações do comando `docker run`.

### 1.2 Terminologias

Nesta seção você viu muitas expressões específicas do Docker que podem causar alguma confusão. Então, antes de seguirmos adiante, vamos compreender algumas desses termos frequentemente usados no ecossistema Docker.

- *Imagens  (em inglês, Images)* - O arquivo do sistema e configurações de sya aplicação que são usadas para criar contêiners. Para saber mais sobre uma imagem Docker, execute o comando `docker inspect alpine` (alpine pois se trata do imagem utilizada nesta etapa do laboratório). Na demonstração acima, você usou o comando `docker pull`para baixar a imagem **alpine**. Quando você executou o comando `docker run hello-world`, por trás dos panos o Docker também executou o comando `docker pull` para baixar a imagem **hello-world**.
- *Contêiners (em inglês, Containers)* - Istancias Docker em execução - as aplicações rodam em contêiners. Um contêiner inclui uma aplicaçãoe todas as suas dependências. Um contêiner compatilha o kernel com outros contêiners e é executado como um processo isolado no sistema operacional hospedeiro (host). Você criou um contêiner usando o comando `docker run` que usando a imagem do alpine linux que havia baixado previamente. Uma lista com os contêiners em execução pode ser obtida usando o comando `docker ps`.
- *Docker daemon* - O serviço executado em segundo plano no host que gerencia o construção (build), a execução e o distribuição (deploy) dos contêiners.
- *Cliente Docker (em inglês, Docker client)* - O utilitário de linha de comando que possibilita que o usuário interaja com o Docker daemon.
- *Docker Hub* - Um [repositório (registro)](https://hub.docker.com/explore/) de imagens Docker. Trata-se de um repositório com todas as imagens Docker disponíveis. Você usará posteriormente neste tutorial.

## Proximos passos
Para a próxima etapa deste tutorial, vá para: [2.0 Aplicativo web com Docker](chapters/webapps_pt-br.md)































