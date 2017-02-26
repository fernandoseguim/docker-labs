## Configurações

### Pré-requisitos
Não há a necessidade de alguma habilidade específica para este tutorial além do conheimento básico sobre linhas de comando e o uso de um editor de texto nativo do seu sistema operacional (como o notepad para windows ou gedit para linux/ubuntu). Uma experiência anterior em desenvolvimento de aplicativos pode ser útil ao longo deste tutorial, mas não é essencialmente necessária. À medida que evoluirmos ao longo deste tutorial, utilizaremos o [Docker Hub](https://hub.docker.com/), portanto é recomendado que crie uma conta caso ainda não possua.

### Configurando o seu computador
Configurar o Docker em seu sistema operacional favorito é uma tarefa muito fácil.

O guia de início no Docker contém instruções detalhadas para tê-lo configurado no [Mac](https://docs.docker.com/docker-for-mac/), [Linux](https://docs.docker.com/engine/installation/linux/) e [Windows](https://docs.docker.com/docker-for-windows/).

No entanto se preferir seguir um guia traduzido pode seguí-lo por aqui:

* [como instalar o Docker no windows](setup/windows_pt-br.md)
* [como instalar o Docker no linux/ubuntu](setup/linux_pt-br.md)
* [como instalar o Docker no mac](setup/mac_pt-br.md)

*Se você estiver usando Docker para Windows* certifique-se de que [compartilhou sua unidade de disco](https://docs.docker.com/docker-for-windows/#/shared-drives) para que esteja disponível para seus containers.

**NOTA IMPORTANTE** Se você estiver usando uma versão antiga do Windows ou MacOS você pode precisar usar [Docker Machine](https://docs.docker.com/machine/overview/)

*Todos os comandos funcionam em bash ou Poweshell no Windows*

Uma vez concluída a instalação do Docker, você poderá testá-la executando o seguinte comando:

```
$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
03f4658f8b78: Pull complete
a3ed95caeb02: Pull complete
Digest: sha256:8be990ef2aeb16dbcb9271ddfe2610fa6658d13f6dfb8bc72074cc1ca36966a7
Status: Downloaded newer image for hello-world:latest

Hello from Docker.
This message shows that your installation appears to be working correctly.
...
```

## Próximos passos
Para a próxima etapa deste tutorial, vá para: [1.0 Rodando o seu primeiro container](chapters/alpine_pt-br.md)

