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
* [UpperCamelCase](http://wiki.c2.com/?UpperCamelCase) ou [PascalCase](http://wiki.c2.com/?PascalCase)
* [lowerCamelCase](http://wiki.c2.com/?LowerCamelCase) _ou apenas camelCase_


Nomenclatura
==============================

Todos os nomes devem estar em inglês.

## Métodos

**Capitalização:** PascalCase

Os métodos devem expressar uma ação, ou seja, devem ser verbos ou começar com verbos.
Exemplos:

Ação | Certo :+1: | Errado :-1:
-- | -- | --
Envia um email | `SendEmail()`, `Send()` | `EmailSender()`
Inicializar alguma coisa | `Initialize()`, `Setup()` | `Initialization()`, `Bootstrapper()`
Fazer café | `MakeCoffee()` | `CoffeeMachine()`

### Variáveis locais

**Capitalização:** camelCase

_O escopo de variáveis ​​locais devem ser mantidos a um mínimo (Effective Java Item 29). Ao fazer isso, você aumenta a legibilidade e manutenção de seu código e reduzir a probabilidade de erro. Cada variável deve ser declarada no bloco mais interno que inclui todos os usos da variável._

_As variáveis ​​locais devem ser declaradas no momento da sua primeira utilização. Quase todas as declarações de variáveis locais devem conter um inicializador. Se você ainda não tem informações suficientes para inicializar uma variável de forma sensata, você deve adiar a declaração até que tenha as informações necessárias para isso._ - ([Android code style guidelines](https://source.android.com/source/code-style.html#limit-variable-scope))

Apesar desse trecho ter sido retirado de um artigo referente ao Java, se encaixa perfeitamente no contexto de qualquer linguagem, porque é referente à legibilidade do código. 

Variáveis locais, como qualquer outro membro da classe, devem ter um nome claro do papel delas no algoritmo.
Exemplo:

Papel da variável | Nome certo :+1: | Nome errado :-1:
-- | -- | --
Modelo da entidade Student | `student`, `studentModel` | `s`, `sm`, `stdnt`
`Decimal` que representa um valor financeiro | `amount` | `a`, ``
Fazer café | `MakeCoffee()` | `CoffeeMachine()`

## Propriedades

**Capitalização:** PascalCase

Sempre utilizar propriedades para membros públicos de uma classe, mesmo quando não forem propriedades full. Alguns motivos para isso:

* Possibilidade de personalizar os modificadores de acesso;
* Herança: não é possível ter `fields` em interfaces, assim como não é possível sobrescrever `fields` da classe base.
* Adicionar lógica no `getter` e no `setter` não quebraria o código existente;
* Data bindings são feitos apenas com propriedades.
* Rastreabilidade: debugar apenas quando a propriedade alterar o valor - adicionar breakpoint no `setter`. Fazer uma validação do conteúdo antes de retorná-lo - adicionar validação no `getter`. Até mesmo o Visual Studio mostra o número de ocorrências da propriedade (coisa que não faz com os `fields`), facilitando o desenvolvimento.

:warning: _Propriedades full devem ter a propriedade com o nome em PascalCase e o `field` correspondente privado  e em camelCase._

## Campos (`fields`)

**Capitalização:** camelCase para `fields` privados e PascalCase para `fields` públicos.

Devem ser evitados. Em projetos como WPF e Windows Forms, os _code behinds_ utilizam campos como componentes visuais. Nesse caso, os componentes visuais devem:

* Seguir a nomenclatura: **ux + sigla para o componente + nome do componente**. O nome do componente deve ter 3 caracteres para nomes simples, 4 caracteres para nomes compostos e conter apenas consoantes.
* Serem sempre privados, com exceção de alguma necessidade de regra de negócio .

Exemplos:

Tipo do componente visual | Nome 
-- | -- 
Label | `uxLblClientName` 
Button | `uxBtnRegister` 
TextBox | `uxTbxClientName` 
RadioButton | `uxRbtnOptionFemale` 
ComboBox | `uxCbbxClientJobList`

:warning: _Em situações em que a classe possui muitos atributos (lidando com GUI, por exemplo), é aconselhável utilizar o prefixo _ antes dos campos privados, apenas para melhorar a legibilidade do código. Se essa prática for utilizada, é importante utilizá-la em todas as classes do projeto. Exemplos: `_labelContent`, `_canRegister` e etc._

## Eventos

**Capitalização:** PascalCase

Existem duas partes: as **variáveis que guardam os eventos** e os **métodos que serão executados** quando a variável for acionada.

### Variáveis de eventos (_triggers_)

Os `EventHandler`s devem ter nome da ação a ser feita. 

Exemplos:

Ação | Nome 
-- | -- 
Quando algo for logado | `Logged` 
Quando uma propriedade foi alterada | `PropertyChanged` 
Antes de uma atualização de sistema | `AfterSystemUpdate` 
Quando a aplicação está esperando por uma interação do usuário | `WaitingForUserConfirmation`

### Métodos handlers de algum trigger (_actions_)
    
Os métodos devem ter o nome composto por: **On + nome do _trigger_** (ação simples) ou **On + informação complementar + if/when (opcional) + nome do _trigger_** (ação composta ou específica). 

Exemplos:  
    
Ação | Nome do _trigger_ | Nome da _action_ 
-- | -- | --
Quando algo for logado | `Logged` | `OnLogged` ou `OnSendLogsToServerWhenLogged`
Quando uma propriedade foi alterada | `PropertyChanged` | `OnPropertyChanged` ou `OnValidateValueWhenPropertyChanged` 
Antes de uma atualização de sistema | `BeforeSystemUpdate` | `OnBeforeSystemUpdate` ou `OnBackupBeforeSystemUpdate`
Quando a aplicação está esperando por uma interação do usuário | `WaitingForUserConfirmation`| `OnWaitingForUserConfirmation` ou `OnShowMessageIfWaitingForUserConfirmation`

## Constantes

**Capitalização:** PascalCase

Constantes devem ter um nome bem claro da informação que ela representa, por exemplo:

Informação | Nome
-- | --
Time out em segundos | TimeOutInSeconds
Expressão regular para CPF | CpfRegexPattern
Valor _default_ para o número de tentativas de conexão | DefaultNumberOfConectionTries

:warning: _Se você possui muitas constantes relativas a um único assunto, considere utilizar um [arquivo de recurso](#arquivos-de-recurso)._

## Enumeradores

## Extension method

## Prefixos ou sufixos especiais
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
- Regions

Guideline de boas práticas
==============================

## strings
    . concatenação simples
    . concatenação em loop
        StringBuilder

## tipos nativos

## var

## boolean

## if compacto

## operações inline

## valores mágicos

## utilização de atributos

## try catch

## arquivos de recurso

## numero de parâmetros enviados a um método

## tamanho da linha
    . Pegar do joaozinho

## sealed

## Control flow
    - for
    - foreach
    - while
    - do-while
    - if, else, else-if
    - switch

## LINQ

## argumento de evento

Documentação
==============================

- Documentação e comentários

Testes de unidade
==============================
    
- Testes de unidade

 