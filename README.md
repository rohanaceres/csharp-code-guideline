# csharp-code-guideline

~descrição~

Índice
==============================

* [Conhecimentos básicos](#conhecimentos-básicos)
* [Nomenclatura](#nomenclatura)
* [Classes.cs](#classes)
* [Guideline de boas práticas](#guideline-de-boas-práticas)
* [Testes de unidade](#testes-de-unidade)

Conhecimentos básicos
==============================

Nomenclatura
==============================

- Métodos
    . variáveis locais
- Propriedades
    . gets e sets
- Campos
    . ux
- Eventos
    . Handlers e métodos de handling
- Constantes
- Enumeradores
- Extension method
- Prefixos ou sufixos especiais
    . pages
    . resources
    . abstract
    . interfaces

Classes
==============================

- Algumas definições
    - Membro: todos os métodos, construtores, propriedades e campos de uma classe.
- Estrutura da classe
    - partes de um .cs
        . includes
        . namespace
            . constantes
            . campos estáticas
            . propriedades estáticas
            . campos - se for membro de propriedade full, colocar o membro privado imediatamente acima da propriedade correspondente.
            . propriedades de interface
            . propriedades 
            . construtor
            . métodos estáticos 
            . métodos de interface
            . métodos da classe
        . extension methods que serão utilizados SOMENTE naquela classe
        (!) Todos os membros são ordenados seguindo a regra - public, internal, private
        (!) Nunca deixar um membro da classe sem modificador de acesso!
- Ciclo de vida da classe
- Generics e tipos genericos

Guideline de boas práticas
==============================

- strings
    . concatenação simples
    . concatenação em loop
        StringBuilder
- tipos nativos
- var
- boolean
- if compacto
- operações inline
- valores mágicos
- utilização de atributos
- try catch
- arquivo de recurso
- numero de parâmetros enviados a um método
- tamanho da linha
    . Pegar do joaozinho
- sealed
- Control flow
    - for
    - foreach
    - while
    - do-while
    - if, else, else-if
    - switch
- LINQ

Documentação
==============================

- Documentação e comentários

Testes de unidade
==============================
    
- Testes de unidade

 