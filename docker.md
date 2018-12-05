# O que é Docker

O Docker é gerenciador de containers que aproveita somente a estrutura básica e necessária do kernel do sistema operacional do seu host de forma que não é necessário a instalação de todo o sistema.

# Gerando container a partir de uma imagem

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




 
