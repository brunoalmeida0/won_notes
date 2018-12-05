# Programação orientada a objetos

É um paradgma de programação que promove a abstração, reuso, modularidade e Isolamento de responsabilidades


## Conceitos básicos
### Abstração
É a capacidade de tranformar um objeto real em uma ideia, em atributos e funcionalidades capazes de serem descritas

### Classes
É a unidade básica de abstração em Java é um "Modelo" para os objetos

### Atributos
Os atributos são as caracteristicas que pertencerão ao objeto.

### Métodos
São "ações" a serem realizadas pelo objeto.
É necessário expecificar o tipo do retorno do método, se não houver retorno. Também é possível receber ou não argumentos.


### Tipo
Java é uma linguagem fortemente tipada.

#### Tipo primitivo
```int``` - Armazena um valor do tipo inteiro
...
#### Tipos não primitivos**
```String``` - 

### Objetos
São concretizações de abstrações da classe.
A classe seria como um molde, e o objeto será derivado dessa classe.

``` Cat gato = new Cat(); ```


### Construtores
É um método especial que será executado no momento da criação do objeto. É possível passar parâmetros para o construtor, caso seja necessário executar alguma ação no momento da criação do objeto.


### Interfaces
É um contrato de classe. Todo mundo que implementa a interface tem que implementar os métodos presentes na interface.
Sua sintaxe é parecida com uma classe, porém não recebe parâmetros e seus métodos não tem corpo, apenas as assinaturas.


```
public interface GatoViralatas {
    void reirarLata(Lata lata);
}

//implementação
public class MandaChuva implements GatoViralatas {
    void revirarLata(Lata lata);
    lata.revirar();
}
```

### Sobrecarga
É o conceito de dar mais de uma entrada para uma mesma função.
O que diferencia uma chamada de função de outra é a quandidade e o tipo de argumentos recebidos.

### Herança
Herança de classes é o conceito de uma classe herdar TODOS os atributos e métodos da classe pai. Não é necessário expecificar tais atributos e métodos na classe filha.

Caso um método necessite ser reescrito, o ```@override``` é necessário para indicar.

### Polimorfismo
É a capacidade de um objeto de ter vários tipos.

```
GatoViralatas gato1 = new MandaChuva();
GatoViralatas gato2 = new Batatinha();
```

Problema: os métodos de MandaChuva e Batatinha não poderão ser acessados.
Motivação: Um método poderá identificar todos os "GatoViralatas" sem precisar filtrar todos os tipos de gatos como MandaChuva e Batatinha.

É possível retomar ao tipo do objeto fazendo um Cast

### Encapsulamento
É o conceito de modularizar o código. Dentro de cada classe só há o necessário para seu funcionamento. Haverão atributos e métodos que não precisam ser expostos.

# Java

## Características 
Hibrida = Compilada e interpretada, o que permite ela ser multiplataforma.

Orientada a objeto

Tipagem forte, estática e estrutural

Portavel (WORE - Write once, run everywhere)


## Arqueitetura


## Anotações aleatórias 
Singleton***
Arquitetura do Java

ORM***

A solutis utiliza Java 8

Closure - passagem de função e retorno de função

google guava
