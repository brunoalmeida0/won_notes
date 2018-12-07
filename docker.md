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




















 

## Gerando container a partir de uma imagem

As imagens podem ser entendidas como geradores de containers, é a partir dela que o container será criado.

Um exemplo que ilustra bem isso é a imagem "hello-world" presente no repositório de imagens Docker Hub (onde estão presentes as imagens oficiais).


``` docker run hello-world ```

Ao executar esse comando o docker busca a imagem localmente, se ela não for encontrada, o docker buscará no Docker Hub.

Para visualizarmos os containers que estão em execução é necessário executar o comando
``` docker ps ```, porém, neste caso o hello-world não estará mais lá, já que a sua função é somente printar no terminal uma mensagem e finalizar sua execução.

Para que todos os containers já executados no host sejam visualizados, a tag  ```-a``` deve ser acrescentada:
``` docker ps -a ```


O comando
``` docker images ``` 
 mostra todas as imagens presentes na máquina. "Uma imagem é um container parado". Quando a imagem é executada ela é transformada em um container em execução.




 
