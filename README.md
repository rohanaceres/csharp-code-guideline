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

Algumas leituras importantes, porque são conhecimentos fundamentais no dia a dia do desenvolvedor (por mais que algumas vezes el@ nem saiba disso).

Decidi colocar esses itens (que irão ser complementados com o tempo), porque além de ser importante ter um código consistente lógicamente, legível e documentado, é importante entender alguns conceitos que estão implícitos no desenvolvimento. Você não precisa ser um expert em nenhuma dessas tecnologias e conceitos (será? talvez você precise), mas apenas entender basicamente como elas funcionam e de que forma ela impacta o seu trabalho.

* [GRASP](https://en.wikipedia.org/wiki/GRASP_(object-oriented_design))
* [SOLID](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design))
* Alguns [protocolos de comunicação](https://pt.wikipedia.org/wiki/Protocolo_(ci%C3%AAncia_da_computa%C3%A7%C3%A3o)) básicos:
    * [TCP/IP](https://en.wikipedia.org/wiki/Internet_protocol_suite)
    * [HTTP](https://pt.wikipedia.org/wiki/Hypertext_Transfer_Protocol), [HTTP/2](https://en.wikipedia.org/wiki/HTTP/2) e [HTTPS](https://pt.wikipedia.org/wiki/Hyper_Text_Transfer_Protocol_Secure)
        - [REST](https://pt.wikipedia.org/wiki/REST)
        - [SOAP](https://pt.wikipedia.org/wiki/SOAP)

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

 