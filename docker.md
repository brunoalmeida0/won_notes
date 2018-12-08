# O que é Docker

O Docker é gerenciador de containers que aproveita somente a estrutura básica e necessária do kernel do sistema operacional do seu host de forma que não é necessário a instalação de todo o sistema.

## Vantagens do Docker sobre VM
O docker utiliza do próprio kernel do SO host para gerar seus containers e rodar o necessário para seu funcionamento. Já a VM emula todo um ambiente de um novo SO completamente independente do SO host. Essa capacidade dos containers utilizarem recursos mínimos do seu host gera uma eficiência muito maior em relação a quantidade de memória e processamento necessários para seu funcionamento. Um exemplo disso é a inicialização de uma VM, que demora em torno de um minuto, já um container pode ser iniciado em milissegundos.

# Conceitos importantes

## Containers
Um container pode ser descrito como uma segregação de processos no mesmo kernel, ou seja, gera um isolamento de processos relacionados ao funcionamento do container do restante do SO host, utilizando somente o necessário dele.

A partir de uma imagem, que é um "modelo", um container pode ser criado.

Containers são ambientes leves e portáteis onde aplicações são executadas, todos os binários e bibliotecas necessárias para execução de uma determinada aplicação é completamente encapsulado no container. 

Uma boa prática é modularizar cada um dos containers, ou seja, ter um container para o banco de dados, um para o back-end e um para o front-end torna cada um deles muito mais flexível e livre para startar somente processos realmente necessários para a aplicação. 

## Imagens

Imagens são modelos de sistema de arquivo Only Read usado para criar containers. A grosso modo, imagens são classes e containers são objetos em orientação a objetos.

As imagens podem ser criadas através de dois processos, *build* e *commit*. *commit* não é considerado uma boa prática, já que a imagem é criada sem deixar rastros, o que impossibilita sua replicação e torna mais difícil sua manutenção, já com *build* um arquivo de registro é criado com todos os passos realizdos para a criação da imagem.

Existem vários repositórios para registro de imagens na internet, o oficial e mais famoso é o [Docker Hub](https://hub.docker.com/).

As imagens são compostas por uma ou mais Layers, cada Layer representa uma mudança, desde a criação ou edição de um arquivo até o deploy de uma aplicação, no sistema de arquivo. O sistema de layers possibilita o reuso da imagem de maneira mais eficiente, já que uma imagem criada com algumas configurações que serão utilizadas por vários containers poderá carregar a configuração desejada em todos eles. Como a imagem é Only Read, apenas a ultima camada é disponibilizada para alteração.

Com esse sistema de Layers, imagens podem ser compostas a partir de outras imagens.

## Arquitetura
A arquitetura do Docker se baseia em três camadas, uma camada de *client* onde é possível interagir com os containers e o *daemon* através de linha de comando, API REST ou o Kitematic que é uma ferramenta gráfica. Uma camada de Host que se baseia no SO host, que é onde se localiza o *daemon/docker server/docker engine*, os containers e as imagens retiradas do *registry* e a ultima camada é o próprio *Registry* que fica na núvem e o Docker Hub é um exemplo disso.

# Instalação 

## Visão geral

__Linux:__ Como o Docker é baseado na LXC, ele utiliza o kernel do SO Host de fato, onde todas as camadas da Arquitetura (exeto o *Registry*) serão executadas.

__MacOS X:__ Para uso do Docker no Mac é necessário que haja uma criação de uma Linux VM que irá encapsular a *Docker Engine (Daemon)* e seus containers, o *Docker Client* rodará no OS Host e se comunicará normalmente com o *Daemon*, todo esse processo já é inicializado no monento da instalação do Docker.

__Windows:__ O processo de instalação do Docker no Windows 10 Pro e versões mais atuais se assemelha com a instalação do Linux graças ao Windows Subsystem For Linux. Já versões mais antigas utilizarão um modelo mais parecido com o do MacOS X, com o encapsulamento do *Daemon*. 

# Comandos importantes

> Run

```docker container run <nome da imagem>```

Esse comando é utilizado para *startar* um container.
Esse comando é a junção de 4 outros comandos:
Caso a imagem não existir locamente, será feito um ```docker pull <nome da imagem>``` automáticamente e a imagem será baixada;

```docker container create``` que é a criação do container;
```docker container start``` que é a inicialização do container;
```docker container exec``` que é a execução do container.

O ```run``` SEMPRE cria novos containers.

```docker run -it debian bash```

Esse exemplo irá criar, inicializar e executar o container, e a flag ```-it``` pode ser dividida em ```--i``` (modo interativo) e ```--t``` (acesso ao terminal).

> rm

```docker --rm <nome do container>```

O ```--rm``` irá remover o container desejado, há também variações desse comando como:

```docker run --rm debian bash --version```

Nesse segundo exemplo, o container será criado, startado, executado e no final de sua execução interativa ele irá ser removido. 

> --name

```docker run --name mydeb debian```

Nomeia um container. Não pode existir dois containers com o mesmo nome.




# Modo interativo
É um modo de executar um container de forma interativa, diferente do modo tradicional do *Daemon* onde o container roda em background executando o seu conteúdo com um banco de dados ou outro serviço.

O modo interativo é interessante para realizar testes e visualizar o que está ocorrendo dentro do container.

> Exemplo de comando interativo:

```docker container run debian bash --version```

Após a execução do ```run```, será executado o comando ```bash --version``` e o container será parado, pois a função a ser desempenhada foi passada.


# Mapeamento de portas dos containers

A comunicação entre containers e entre o SO Host é fundamental para a utilização e desenvolvimento de aplicações e serviços.

Um exemplo de exposição de uma porta do container para o Host é:

```docker run -p 8080:80 nginx```

Onde a flag ```-p``` expõe para a maquina host a porta 8080 que é mapeada para a porta 80 que está startada no container, que é a porta padrão startada pelo ngnix que também é a padrão do HTTP.

Para acessar o conteúdo deste container é necessário acessar o ```http://localhost:8080```

# Mapeamento de diretórios para o container

Para um container docker acessar um diretório do host é necessário que o caminho da pasta local seja definido, assim como o diretório do container que irá espelhar.

```docker run -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html nginx```

Onde ```-v``` é a flag que expecifica o volume a ser mapeado.


# Rodando um servidor em background

Essa é uma das principais funcionalidades do Docker.  Com isso temos a possibildade de startar aplicações e servidores em background e conseguir fazer eles se comunicarem entre si.

> __Ex:__
> ```docker run -d --name ex-daemon-basic -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html nginx```

Neste comando estamos nomeando um container do *nginx*, mapeando uma porta no host para uma no container e um diretório no host e um no container e com a flag ```-d``` é possível rodar o comando em modo *Daemon*, ou seja, em background.

> __Gerenciamento de containers em background__

>__Start:__ ```docker start <nome ou id do container>```

>__Stop:__ ```docker stop <nome ou id do container>```

>__Restart:__ ```docker restart <nome ou id do container>```

>__Ver logs:__ ```docker logs <nome ou id do container>```

>__Ver informações do container:__ ```docker inspect <nome ou id do container>```

>__Ver informações do sistema do container:__ ```docker container exec <nome ou id do container> uname -or```


# Gerenciamento de imagens

```docker pull <nome da imagem>```

Baixa a imagem do repositório remoto

```docker image ls```

Listar imagens baixadas

```docker image rm <nome da imagem>```

Remove a imagem

```docker image inspect <nome da imagem>```

Lista informações sobre a imagem

```docker image tag <nome>:<tag atual ou versão> <nova tag>```

Adiciona uma tag a imagem

```docker image build```

Criar um arquivo descritor e gerar uma imagem

```docker image push```

Faz um push do build para algum repositório

# Docker Hub X Docker Registry

Docker Registry é uma API que permite que imagens sejam enviadas e recebidas. Usuários podem ter sua própria Docker Registry podendo salvar suas próprias imagens. O Docker Hub utiliza o Docker Registry para fazer o fluxo de armazenamento e disponibilização das suas imagens.

# Escrevendo imagens

Para fazer um *build* de uma imagem é necessário criar um arquivo descritor do docker, o __Docker File__.

> Exemplo de Docker File
>
>```FROM nginx:latest ```
>
>```RUN echo '<h1>Hello Wolrd!!</h1>' > /usr/share/nginx/html/index.html```

Esse Dockerfile cria um container a partir da imagem do *nginx* e adiciona mais uma layer ao container, que nesse caso é a criação do arquivo *index.html* e a adição de conteúdo dentro dele.

Para fazer o build dessa imagem é necessário usar o seguinte comando:

```docker image build -t ex-simple-build .```

Onde *build* é o comando principal, *-t* define o nome da tag, e o *"."* é o caminho para o arquivo Dockerfile.

Com isso é possível verificar com o ```docker image ls``` que a imagem criada está sendo listada.

Para executar um container a partir da imagem criada é necessário simplesmente um *run*

```docker run -p 80:80 ex-simple-build```

## Recebendo argumentos no Dockerfile

Podemos receber argumentos no Dockerfile e assim adequar o container criado ao problema ser resolvido.

> Exemplo de Dockerfile recebendo argumentos:
>
>```FROM debian```
>```LABEL maintainer 'Bruno <brunoalmeida>'```
>
>```ARG S3_BUCKET=files```
>```ENV S3_BUCKET=${S3_BUCKET}```

O argumento neste caso é chamado de *S3_BUCKET*.

Para passar parâmetros para esse argumento, no momento do build é necessário expecíficar:

```docker image build --build-arg S3_BUCKET=myapp -t ex-arg .```

O parâmetro recebido foi a string *myapp*

Para exibir a variável deste exemplo:

```docker run ex-arg bash -c 'echo $S3_BUCKET'```
