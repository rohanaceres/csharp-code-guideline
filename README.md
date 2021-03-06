# csharp-code-guideline

Esse documento descreve algumas boas práticas de organização e legibilidade do código para a linguagem C#. 

Índice
==============================

* [Conhecimentos básicos](#conhecimentos-básicos)
* [Formatação](#formatação)
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

Formatação
==============================

## Chave

**Sempre utilizar chave embaixo** em:

* Namespaces
* Classes
* Métodos
* _Getter_ e _setter_ (se houver implementação deles)
* `if`, `else` e `if-else`
* `do-while` e `while`
* `for` e `foreach`

**Utilizar chave em cima** em:

* `if`, `else` e `if-else` **in-line**: se algum deles não for in-line, utilizar chave embaixo em todos.
* _Getter_ e _setter_ **in-line**

:warning: _Sempre utilizar chaves, mesmo quando o corpo tiver apenas uma linha._

**Certo :+1:**:

```
namespace SomeNamespace
{
    public sealed class SomeClass
    {
        public int SomeInt { get; set; }

        public void SomeMethod ()
        {
            if (someBool == true) { return; }

            for (int i = 0; i < 10; i++)
            {
                // Do something
            }
        }
    }
}
```

**Errado :-1:**:

```
namespace SomeNamespace {
    public sealed class SomeClass
    {
        public int SomeInt 
        { 
            get; 
            set; 
        }

        public void SomeMethod ()
        {
            if (someBool == true) 
                return; 

            for (int i = 0; i < 10; i++)
            {
                // Do something
            }
        }
    }
}
```

## this

Sempre utilizar o `this` para métodos, campos e propriedades da classe.

## Espaçamento

A identação é feita com tabs e o espaçamento entre operadores deve ter um espaço em branco.

**Certo :+1:**:

* `public sealed class SomeClass : ISomeClass`
* `int sum = a + b`
* `public void SomeMethod (int a, double b)`
* `if (someBool == true)`
* `while (someBool == true);`
* `for (int i = 0; i < 10; i++)`

**Errado :-1:**:

* `public sealed class SomeClass:ISomeClass`
* `int sum=a+b;`
* `public void SomeMethod(int a,double b)`
* `if(someBool)`
* `while(someBool == true);`
* `for (int i=0; i<10; i++)`

## Chamadas em cadeia

Alguns padrões de projeto utilizam a chamada de métodos encadeados como forma de produzir o output esperado. Alguns exemplos disso são:

- LINQ
- Builder

Esse tipo de chamada deve ser feita separando cada método encadeado em linhas diferentes:

Exemplo em chamada encadeada:

```
IEnumerable<SelectListItem> stores = database.Stores
        .Where(store => store.CompanyID == curCompany.ID)
        .Select(store => new SelectListItem { Value = store.Name, Text = store.ID });
```

Exemplo em query LINQ:

```
IEnumerable<SelectListItem> stores =
        from store in database.Stores
        where store.CompanyID == curCompany.ID
        select new SelectListItem { Value = store.Name, Text = store.ID };
```

Nomenclatura
==============================

Todos os nomes devem estar em inglês.

## Siglas

Siglas devem ser tratadas como palavras comuns, ou seja:

Certo :+1: | Errado :-1:
--- | ---
clientCpf | clientCPF
sqlQuery | SQLQuery
myDB | myDb

## Métodos

**Capitalização:** PascalCase

Os métodos devem expressar uma ação, ou seja, devem ser verbos ou começar com verbos.
Exemplos:

Ação | Certo :+1: | Errado :-1:
--- | --- | ---
Envia um email | `SendEmail()`, `Send()` | `EmailSender()`
Inicializar alguma coisa | `Initialize()`, `Setup()` | `Initialization()`, `Bootstrapper()`
Fazer café | `MakeCoffee()` | `CoffeeMachine()`

### Variáveis locais

**Capitalização:** camelCase

_O escopo de variáveis locais devem ser mantidos a um mínimo (Effective Java Item 29). Ao fazer isso, você aumenta a legibilidade e manutenção de seu código e reduzir a probabilidade de erro. Cada variável deve ser declarada no bloco mais interno que inclui todos os usos da variável._

_As variáveis locais devem ser declaradas no momento da sua primeira utilização. Quase todas as declarações de variáveis locais devem conter um inicializador. Se você ainda não tem informações suficientes para inicializar uma variável de forma sensata, você deve adiar a declaração até que tenha as informações necessárias para isso._ - ([Android code style guidelines](https://source.android.com/source/code-style.html#limit-variable-scope))

Apesar desse trecho ter sido retirado de um artigo referente ao Java, se encaixa perfeitamente no contexto de qualquer linguagem, porque é referente à legibilidade do código. 

Variáveis locais, como qualquer outro membro da classe, devem ter um nome claro do papel delas no algoritmo.
Exemplo:

Papel da variável | Nome certo :+1: | Nome errado :-1:
--- | --- | ---
Modelo da entidade Student | `student`, `studentModel` | `s`, `sm`, `stdnt`
`Decimal` que representa um valor financeiro | `amount` | `a`, `amt`
Data e hora atual | `currentDateTime` | `dt`, `now`

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
--- | --- 
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
--- | --- 
Quando algo for logado | `Logged` 
Quando uma propriedade foi alterada | `PropertyChanged` 
Antes de uma atualização de sistema | `AfterSystemUpdate` 
Quando a aplicação está esperando por uma interação do usuário | `WaitingForUserConfirmation`

### Métodos handlers de algum trigger (_actions_)
    
Os métodos devem ter o nome composto por: **On + nome do _trigger_** (ação simples) ou **On + informação complementar + if/when (opcional) + nome do _trigger_** (ação composta ou específica). 

Exemplos:  
    
Ação | Nome do _trigger_ | Nome da _action_ 
--- | --- | ---
Quando algo for logado | `Logged` | `OnLogged()` ou `OnSendLogsToServerWhenLogged()`
Quando uma propriedade foi alterada | `PropertyChanged` | `OnPropertyChanged()` ou `OnValidateValueWhenPropertyChanged()` 
Antes de uma atualização de sistema | `BeforeSystemUpdate` | `OnBeforeSystemUpdate()` ou `OnBackupBeforeSystemUpdate()`
Quando a aplicação está esperando por uma interação do usuário | `WaitingForUserConfirmation()`| `OnWaitingForUserConfirmation` ou `OnShowMessageIfWaitingForUserConfirmation()`

## Constantes

**Capitalização:** PascalCase

Constantes devem ter um nome bem claro da informação que ela representa, por exemplo:

Informação | Nome
--- | ---
Time out em segundos | TimeOutInSeconds
Expressão regular para CPF | CpfRegexPattern
Valor _default_ para o número de tentativas de conexão | DefaultNumberOfConnectionTries

:warning: _Se você possui muitas constantes relativas a um único assunto, considere utilizar um [arquivo de recurso](#arquivos-de-recurso)._

:warning: _Sempre utilize o nome da classe ao utilizar uma constante, para facilitar a leitura e_ code review _do código. Exemplo:_

```
public sealed class Dog 
{
    public const int NumberOfPaws = 4;

    // Some dog code ...

    public void Walk ()
    {
        for (int i = 0; i < Dog.NumberOfPaws; i++)
        {
            this.Move(this.Paws[i]);
        }
    }
}
```


## Enumeradores

**Capitalização:** PascalCase

O nome da classe deve ser composto por um dos padrões abaixo: 

* Objetivo do enum + **Code**
* Objetivo do enum + **Type**
* Objetivo do enum + **Mode**

Exemplos:

Objetivo do enum | Nome
--- | ---
Tipos de transação financeira | `TransactionType`, `TransactionMode`
Cores | `ColorCode`
Tipos de protocolo de comunicação | `CommunicationType`, `CommunicationMode`
Status de algum serviço ou aplicação | `ApplicationStatusCode`

Devem possuir sempre um valor **Undefined = 0**, motivos para isso:

* Evitar que o valor de um `enum` seja usando sem que o valor dele seja definido
* Evitar que o valor default do enum (`default(EnumName)`)

Exemplo prático:

```
public enum ColorCode
{
    Undefined = 0,
    White,
    Red,
    Green,
    Blue,
    Black
}
```

## Extension method

**Capitalização:** PascalCase

Se o `extension method` for utilizado apenas em uma classe, colocar ele no mesmo arquivo que a classe a ser complementada. Se ele for para ser utilizado globalmente, coloque na pasta raiz da classe a ser complementada. 

:warning: _Não crie uma pasta **Extension** e coloque todos os `extension methods` lá._

Devem ser nomeados como: 

* Nome da classe a ser extendida + **Extension**

Exemplo prático:

```
public static class IntExtension
{
    public static int Sum (this int a, int b)
    {
        return a + b;
    }
    public static int Subtract (this int a, int b)
    {
        return a - b;
    }
    public static int Multiply (this int a, int b)
    {
        return a * b;
    }
    public static double Divide (this int a, int b)
    {
        return a / b;
    }
}
```

## Prefixos ou sufixos especiais

Para tipos de arquivos, utilizar: **nome da classe + nome do arquivo**. 

Exemplos:

* `Page`: função + **Page**. Exemplo: `RegisterPage`
* `Resource`: função + **Resource**. Exemplo: `RegularExpressionResources`.
* `UserControl`: função + **UserControl**. Exemplo: `AdvancedSettingsUserControl`.

Para `interface` e `abstract`:

* Classes abstratas: **Abstract** + nome da classe. Exemplo: `AbstractPaymentService`.
* Interfaces: **I** + nome da classe. Exemplo: `IPaymentService`.

Classes
==============================

**Capitalização:** PascalCase

## Algumas definições

**Membro**: todos os métodos, construtores, propriedades e campos de uma classe.

## Estrutura da classe

### Partes de um `.cs`

Separei o corpo de um arquivo `.cs` como se fosse um XML, ou seja: 

```
<includes />
<namespace>
    <class> 
        <constants />
        <br />
        <static-fields />
        <br />
        <static-properties />
        <br />
        <interface-properties />
        <br />
        <full-properties>
            <private-field />
            <property />
        </full-property>
        <br />
        <properties />
        <br />
        <constructors />
        <br />
        <static-methods />
        <br />
        <interface-methods />
        <br />
        <methods />
        <br />
    </class>
    <private-extension-methods />
</namespace> 
```

:warning: _Todos os membros são ordenados seguindo a regra: `public`, `internal`, `private`._
:warning: _Nunca deixar um membro da classe sem modificador de acesso!_

### Ciclo de vida da classe

Se a classe tiver um ciclo de vida bem definido, por exemplo, uma classe de é inicializada, faz alguma ação e depois algum tipo de fechamento, é interessante organizar os métodos de acordo com esse ciclo de vida.

Por exemplo, imagine uma classe `SomeConnection` que tem como objetivo verificar se é possível conectar, estabelecer conexão, fechar conexão e liberar memória. Para tanto, é interessante que a ordem dos métodos no arquivo da classe estejam organizadas seguindo esse fluxo. Ou seja:

```
public sealed class SomeConnection : IDisposable
{
    public bool CanConnect ()
    {
        // Implementation...
    }
    public void Connect ()
    {
        // Implementation...
    }
    public void Disconnect ()
    {
        // Implementation...
    }
    public void Dispose()
    {
        // Free memmory...
        GC.SuppressFinalize(this);
    }
}
```

### Regions

:warning: _**Evitar ao máximo utilizar!** Regions escondem complexidade._

Guideline de boas práticas
==============================

## Tipos nativos

Sempre utilizar os tipos nativos, e não seus respectivos _wrappers_.

Certo :+1: | Errado :-1:
--- | ---
`string` | `String`
`short` | `Int16`
`ushort` | `UInt16`
`int` | `Int32`
`uint` | `UInt32`
`long` | `Int64`
`ulong` | `UInt64`
`decimal` | `Decimal`

## Strings

### Concatenação simples

A concatenação simples de strings deve ser feita com o método `Format()`, por exemplo:

```
string message = string.Format("Olá, {0}!", client.Name);
Console.WriteLine(message);
``` 

### Concatenação em loop

Concatenações em loop e manipulação de muitas strings deve ser feita utilizando a classe `StringBuilder`. Através desse _wrapper_ é possível concatenar string de forma a não perder desempenho.

Exemplo:

```
StringBuilder bookTitleBuilder = new StringBuilder();

foreach (string currentEntry in bookTitles)
{
    bookTitleBuilder.Append(string.Format("{0:S};", currentEntry));
}

string concatBookTitles = bookTitleBuilder.ToString();
```

## `var`

:warning: _Utilizar **somente** quando um valor literal for atribuído à variável e quando o escopo dessa variável `var` for bem pequeno. **Não utilizar em escopos ou métodos longos!**_

## boolean

Sempre nomear como:

* **Is**: `IsSuccess`, `IsRestProtocol` ou `IsSerializable`;
* **Was**: `WasCancelled`, `WasCaptured` ou `WasSerialized`;
* **Has**: `HasAmountToCancel`, `HasContent` ou `HasHttpStatusError`.

É uma boa prática criar propriedades `bool` apenas para facilitar acesso à um dado de forma simplificada. Por exemplo, ao validar se a resposta de um servidor qualquer foi sucesso, é interessante fazer a validação de forma simplificada, como:

```
public sealed SomeResponse
{
    // lot of code...

    public bool IsSuccess
    {
        get { return this.Body != null && this.Body.ErrorList.Count <= 0; }
    }

    // lot of code...
}
```

## valores mágicos

Valores mágicos são tipos nativos (string, int, double etc.) que possuem valores relevantes, usados no meio do código, muitas vezes em mais de um ponto do código.

Nesses casos, é importante que esses valores sejam convertidos em constantes, para que o mesmo valor seja reaproveitado no código e nos testes de unidade. Faça isso por alguns motivos:

* **Reaproveitamento**: se o valor mudar, ele será atualizado em todos os pontos do código;
* **Legibilidade**: o valor mágico vai se tornar muito mais compreensível e legível;
* **Documentação**: constantes devem ser documentadas.

## try catch

Faça a validação de `Exceptions` específicas! Mas **sempre** insira um `try-catch` genérico, para que o erro nunca estoure no cliente. Sempre valide, mesmo que o erro seja desconhecido.

Exemplo:

```
try
{
    // Open file
    // Reads file
    // Cleses file
}
catch (OutOfMemoryException oome) // Specific catch!
{
    // Error! There is insufficient memory to allocate a buffer for the returned string
}
catch (IOException ioe) // Specific catch!
{
    // Error! An I/O error occurs.
}
catch (Exception e) // Generic catch!
{
    // Unexpected and unknown error!
    // This is the most important log.
}
```

## arquivos de recurso

Utilizar arquivos de recursos para:

   - **Mensagens que aparecerão na interface gráfica**: permite o uso (futuro ou não) de multilinguagem.
   - Armazenar **imagens**, **ícones** da aplicação e outros **_visual assets_**.
   - São compilados em **_satellite assemblies_**, melhorando a experiência do usuário (linguagem de acordo com a cultura do computador) e podem ser substituídos sem ter que **recompilar** o projeto.

## numero de parâmetros enviados a um método

Evitar ter métodos e construtores recebendo mais que 4 parâmetros. Nesses casos:

   - Avaliar se os parâmetros têm algo em comum (provavelmente terão!);
   - Criar classes de entrada de dados (_entry data classes_) com as propriedades necessárias.

   > _Functions should have a small number of arguments. No argument is best, followed by one, two, and three. 
   More than three is very questionable and should be avoided with prejudice. 
   [- Robert C. Martin.](http://www.informit.com/articles/article.aspx?p=1375308)_

## tamanho da linha
    
Tente sempre utilizar linhas curtas, de 80 caracteres no máximo. Faça isso para:

- Visualizar o código no **git bash**, sem evitar que o console "corte" o código;
- Visualizar todo o código ao fazer um **code review**;
- **Aumentar o número de editores** de texto em no monitor, em 2 ou 3 janelas;
- Evitar que muita lógica seja inserida em uma única linha (**code density**);
- Melhorar a **indentação** do código.

## sealed

Utilizar o `sealed` sempre que possível (especialmente em classes `internal`), para classes que não poderão ser herdadas de forma lógica. 

:warning: _Cuidado! Uma classe pública pode ser usada e reaproveitata de fora do seu projeto, então, a não ser que seja proposital, mantenha classes públicas **sem** o `sealed`._

## Control flow
    - for
    - foreach
    - while
    - do-while
    - if, else, else-if
    - switch

`// TODO!`

## LINQ

`// TODO!`

## argumento de evento

Documentação
==============================

Alguns tipos de documentação devem ser feitas, como:

### Documentação do projeto

Documentação de **utilização**, em uma linguagem que o público-alvo precisa 
entender. É positivo usar imagens (como tutoriais), fluxogramas ou trechos
de código para deixar mais claro o funcionamento do software ou _lib_.

:warning: Se o projeto for público, _open source_ ou aberto para um grupo 
específico, mas de outra nacionalidade, a documentação terá que ser 
**em inglês**. Fora essas situações, pode ser feita na sua linguagel nativa 
ou fluente.

### Documentação do código

Documentação dos métodos, propriedades, atributos, constantes, classes e 
interfaces. É interessante conhecer as **_tags_ de documentação**, descritas 
[aqui](https://msdn.microsoft.com/en-us/library/5ast78ax.aspx) pela Microsoft.

:warning: Essa documentação será lida sempre que alguém estiver consumindo o código, então
sempre usar acentuação, capitalização e semântica corretamente. 
**Deve ser feita em inglês.**

#### Cuidado!

Não documente de forma viciada. Exemplo do que você **não** deve fazer:

```
/// <summary>
/// Does something.
/// </summary>
/// <param name="appName">Application name.</param>
public void DoSomething(string appName)
{
    // Does something...
}
```

Não seja essa pessoa. Seja essa:

```
/// <summary>
/// Produces something accordingly to the argument received.
/// Validates the result and, if arguments are correct, does something.
/// </summary>
/// <param name="appName">
///     Application name, under UTF-8 and under <see cref="AppSettings.AppNameRegexPattern."/>.
/// </param>
public void DoSomething(string appName)
{
    // Does something...
}
```

### Documentação dos métodos

Documentação interna dos métodos, `getters` e `setters`. Devem descrever a
ação que será executava na linha abaixo.

É útil para comentar informações que só os contribuintes do projeto precisam 
saber, como o porquê de um possível valor mágico, explicação para uma quebra 
de fluxo específica e outros detalhes pertinentes apenas internamente.

Exemplo:

```
public SomethingResult DoSomething()
{
    // Do first action:

    // Validates something:

    // Map and return the result:
}
```

_Sempre com linhas em branco acima do comentário, para deixar claro as etapas do método._

:warning: Pode ser feita na linguagem nativa ou fluente do time.

Testes de unidade
==============================

## Nomenclatura dos métodos

Campos no nome do método:

   - Classe a ser testada
   - [ACT] Método ou propriedade a ser testad@ 
   - [ASSERT] Resultado esperado: sempre começar com **Should** ou **Must**.
   - [ARRANGE] Condicional: começar com **When**, **If** ou **On**.

Vai ficar mais ou menos assim:

```
public void ClasseASerTestada_MetodoASerTestado_ResultadoEsperado_Condiconal ()
{
    // Arrange

    // Act

    // Assert
}
```

Exemplos:

```
public void ReleaseEntryData_Construction_ShouldNotReturnNull() 
{
    // Arrange

    // Act

    // Assert
}
```

```
public void DownloadAgent_Validate_ShouldThrowException_WhenReportWasSuccessfulButSourceUrlIsEmpty
{
    // Arrange

    // Act

    // Assert
}
```

## Nomenclatura para classes de mock

### Classe de mock 

Classe que herda interface a ser mockada e atribui valores aleatórios e válidos. 

   - **Nomenclatura**: Mocked + NomeDaClasse.
   
Exemplo, quando se quer mockar a classe `IHttpClient` do ASP .NET:

```
public class MockedHttpClient : IHttpClient
{
    // Implementation
}
```

### Classe Mocker

São classes que mockam informações, ou seja, criam informações aleatórias e válidas para serem utilizadas em algum caso de teste.

   - **Nomenclatura**: NomeDoTarget + Mocker.

Exemplo: considere que um teste precisa de 10 transações para testar o que é necessário.

```
// Arrange
Transaction[] transactions = new Transaction[10];
for (int i = 0; i < 10; i++)
{
    transactions[i] = TransactionMocker.Generate();
}

// Assert ...
```

```
public class TransactionMocker
{
    public static Transaction Generate ()
    {
        // Generate new transaction
    }
}
```

 
