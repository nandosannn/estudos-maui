# Criando uma ContentPage e entendendo o XAML na prática

## 1. Objetivo da aula

Nesta aula, o objetivo é criar um novo projeto para trabalhar com os tipos de página do .NET MAUI.

Como primeira etapa, o professor escolhe trabalhar com a **ContentPage**, que é o tipo de página mais simples apresentado anteriormente.

Além de criar a página, a aula serve para revisar na prática alguns conceitos da sintaxe do XML/XAML:

- Tags;
    
- Abertura e fechamento de tags;
    
- Atributos;
    
- Componentes;
    
- Classes C#;
    
- Namespaces;
    
- `xmlns`;
    
- `x:Class`;
    
- Propriedade `Title`;
    
- Relação entre XAML e o código por trás da tela.
    

A ideia é entender não apenas como criar uma `ContentPage`, mas também **o que cada parte do arquivo XAML representa**.

---

# 2. Criação de um novo projeto

O professor começa criando uma nova pasta dentro da solução para organizar os novos projetos.

A pasta é chamada de:

```text
EPS02
```

Dentro dela será criado o projeto utilizado para estudar a `ContentPage`.

O projeto é criado utilizando o .NET MAUI.

Durante a criação, o Visual Studio precisa carregar bibliotecas e realizar processos internos de configuração.

---

# 3. Esperar o Visual Studio terminar o carregamento

Um ponto importante apresentado durante a criação do projeto é que o Visual Studio pode apresentar sinais de alerta enquanto ainda está:

- Processando o projeto;
    
- Baixando bibliotecas;
    
- Carregando dependências;
    
- Analisando os arquivos;
    
- Finalizando a configuração.
    

Por isso, a recomendação é **esperar o carregamento terminar antes de começar a modificar o projeto**.

Quando o símbolo de alerta desaparece, significa que o Visual Studio terminou os principais processos de carregamento.

Essa é uma dica prática importante para evitar trabalhar em um projeto enquanto o ambiente ainda está sendo configurado.

---

# 4. Removendo arquivos do projeto

Depois de criar o projeto, o professor remove dois arquivos:

```text
AppShell
MainPage
```

A ideia é construir uma estrutura mais simples, praticamente começando de uma versão inicial do projeto.

Isso permite demonstrar como uma `ContentPage` pode ser criada manualmente e como ela se relaciona com a aplicação.

---

# 5. Criando uma ContentPage

Para criar a página, o professor utiliza a opção de adicionar um novo item no Visual Studio.

Ao acessar:

```text
Botão direito
    ↓
Adicionar
    ↓
Novo item
```

o Visual Studio apresenta diversos templates.

Entre eles estão opções relacionadas ao .NET MAUI.

A aula destaca que existem diferentes tipos de arquivos/templates que podem ser utilizados dependendo do objetivo.

---

# 6. Tipos de arquivos apresentados

Durante a escolha do template, o professor comenta algumas opções.

## Resource Dictionary

O primeiro é o:

```text
Resource Dictionary
```

Esse tipo de arquivo é mais relacionado à organização de recursos visuais e estilos.

Pode ser utilizado para centralizar coisas como:

- Cores;
    
- Estilos;
    
- Aparência;
    
- Configurações visuais de componentes.
    

A aula informa que esse assunto será aprofundado posteriormente.

---

# 7. ContentPage em C#

Também é apresentada uma opção em que a página pode ser construída utilizando apenas C#.

Nesse modelo, a tela e sua lógica ficam concentradas em um único arquivo.

A ideia pode ser representada como:

```text
Arquivo C#
│
├── Construção da interface
└── Lógica da página
```

O professor observa que essa abordagem exige cuidado com organização porque a interface e a lógica ficam juntas.

Não é apresentada como a abordagem principal utilizada atualmente no curso.

---

# 8. ContentPage utilizando XAML + C#

A abordagem mais utilizada apresentada na aula é separar a interface da lógica.

Nesse caso, temos dois arquivos:

```text
MainPage.xaml
MainPage.xaml.cs
```

Cada um possui uma responsabilidade.

### `MainPage.xaml`

Responsável principalmente pela construção visual da página.

```text
XAML
↓
Interface
↓
Componentes
↓
Aparência
```

### `MainPage.xaml.cs`

Responsável pelo código por trás da tela.

```text
C#
↓
Lógica
↓
Comportamentos
↓
Eventos
```

Essa estrutura é chamada na aula de **code-behind**, ou seja, o código por trás da tela.

---

# 9. Por que separar XAML e C#?

A separação permite organizar melhor o projeto.

Podemos visualizar:

```text
MainPage
│
├── MainPage.xaml
│   └── Interface
│
└── MainPage.xaml.cs
    └── Lógica
```

Isso evita colocar toda a construção da interface e toda a lógica no mesmo arquivo.

Essa organização facilita:

- Leitura;
    
- Manutenção;
    
- Alterações na interface;
    
- Alterações na lógica;
    
- Organização do projeto.
    

---

# 10. Criando a MainPage

Para criar a página, o professor escolhe:

```text
ContentPage
```

e dá o nome:

```text
MainPage
```

O Visual Studio gera automaticamente o arquivo:

```text
MainPage.xaml
```

e, na abordagem utilizada, também existe o arquivo correspondente de código:

```text
MainPage.xaml.cs
```

A partir desse momento, temos uma `ContentPage` que pode ser utilizada como a tela principal da aplicação.

---

# 11. MainPage como substituta do AppShell

Como o arquivo `AppShell` foi removido, é necessário configurar a aplicação para utilizar a nova `MainPage` como a página principal.

A ideia é:

```text
Aplicação
   ↓
MainPage
   ↓
ContentPage
```

Assim, quando o aplicativo for executado, a `MainPage` será apresentada.

---

# 12. Estrutura básica de uma ContentPage

A estrutura da `ContentPage` utiliza uma tag XML/XAML.

De forma simplificada:

```xml
<ContentPage>

</ContentPage>
```

A abertura é:

```xml
<ContentPage>
```

e o fechamento é:

```xml
</ContentPage>
```

Dentro dela colocamos os componentes da interface.

Por exemplo:

```xml
<ContentPage>

    <VerticalStackLayout>

        <Label Text="Olá!" />

    </VerticalStackLayout>

</ContentPage>
```

---

# 13. ContentPage é uma tag

Um dos objetivos da revisão é perceber que:

```xml
<ContentPage>
```

é uma **tag**.

O professor relembra que a tag começa com:

```text
<
```

seguida pelo nome:

```text
ContentPage
```

e termina com:

```text
>
```

Portanto:

```text
<ContentPage>
```

representa a abertura da tag.

O conceito é o mesmo apresentado na aula anterior sobre a sintaxe do XML/XAML.

---

# 14. ContentPage também representa uma classe

Um conceito muito importante é que os componentes utilizados no XAML estão relacionados a **classes C#**.

Por exemplo:

```xml
<ContentPage>
```

representa um componente que possui uma classe correspondente.

O mesmo acontece com:

```xml
<VerticalStackLayout>
```

e:

```xml
<Label>
```

Podemos visualizar:

```text
XAML                    C#
--------------------------------
ContentPage      →      Classe
VerticalStackLayout →  Classe
Label            →      Classe
```

Ou seja, os componentes que utilizamos na interface possuem uma implementação em código.

---

# 15. Navegando até a classe

O professor demonstra que é possível utilizar o:

```text
F12
```

no Visual Studio para navegar até a definição da classe.

Ao fazer isso, podemos chegar à implementação do componente e visualizar suas características.

É possível encontrar, por exemplo:

- Propriedades;
    
- Métodos;
    
- Métodos estáticos;
    
- Métodos não estáticos.
    

Isso ajuda a perceber que os componentes do XAML não são elementos "mágicos": eles estão relacionados a classes reais do .NET MAUI.

---

# 16. O .NET MAUI é open source

A aula também comenta que o código-fonte do .NET MAUI está disponível publicamente porque o projeto é **open source**.

Isso significa que é possível consultar sua implementação e estudar como os componentes funcionam internamente.

Assim, podemos sair de uma visão:

```text
"Eu apenas utilizo o Button."
```

para uma visão mais aprofundada:

```text
Button
 ↓
Classe
 ↓
Propriedades
 ↓
Métodos
 ↓
Implementação do .NET MAUI
```

---

# 17. Cabeçalho do XML

No início de um arquivo XAML/XML podemos encontrar uma declaração semelhante a:

```xml
<?xml version="1.0" encoding="utf-8" ?>
```

Essa declaração informa características do documento XML.

No exemplo:

```text
version="1.0"
```

indica a versão do XML.

E:

```text
encoding="utf-8"
```

indica a codificação utilizada.

Essa informação faz parte da estrutura inicial do documento XML/XAML apresentado na aula.

---

# 18. O que são atributos?

Além das tags, temos os **atributos**.

Um atributo é utilizado para fornecer uma informação ou configurar uma característica do componente.

A estrutura básica é:

```text
NomeDoAtributo="Valor"
```

Por exemplo:

```xml
Title="Número da Sorte"
```

Podemos dividir:

```text
Title
  ↓
Nome do atributo

=
  ↓
Operador de atribuição

"Número da Sorte"
  ↓
Valor
```

A aula reforça essa estrutura ao revisar que o atributo é formado pela informação, pelo sinal de igualdade e pelo valor.

---

# 19. Visual Studio auxiliando na leitura do XML

O Visual Studio possui recursos que facilitam a leitura e edição do XAML.

Quando selecionamos uma tag de abertura, o editor consegue destacar a tag correspondente de fechamento.

Por exemplo:

```xml
<VerticalStackLayout>

    <Label />

</VerticalStackLayout>
```

Ao clicar na abertura:

```xml
<VerticalStackLayout>
```

o Visual Studio destaca:

```xml
</VerticalStackLayout>
```

Isso facilita bastante a identificação da estrutura do documento.

Também existem recursos de indentação e destaque visual que ajudam a entender a hierarquia dos componentes.

---

# 20. Hierarquia dos componentes

O destaque visual do Visual Studio ajuda a perceber que os componentes possuem uma relação hierárquica.

Por exemplo:

```xml
<ContentPage>

    <VerticalStackLayout>

        <Label />

        <Button />

    </VerticalStackLayout>

</ContentPage>
```

Podemos representar:

```text
ContentPage
│
└── VerticalStackLayout
    │
    ├── Label
    │
    └── Button
```

Isso significa que:

- `ContentPage` contém o `VerticalStackLayout`;
    
- `VerticalStackLayout` contém o `Label`;
    
- `VerticalStackLayout` contém o `Button`.
    

---

# 21. Namespaces no XAML

Outro ponto importante da aula é a utilização de **namespaces**.

Na estrutura do XAML aparecem declarações como:

```xml
xmlns="..."
```

e:

```xml
xmlns:x="..."
```

O:

```text
xmlns
```

é uma abreviação relacionada a **XML Namespace**.

Namespaces são utilizados para identificar de onde determinados elementos e recursos são obtidos.

A aula destaca que eles podem estar relacionados a:

- URLs;
    
- Assemblies;
    
- Namespaces do próprio projeto;
    
- Bibliotecas de terceiros;
    
- Componentes personalizados.
    

---

# 22. Namespace sem nome

Uma característica importante é que o namespace principal aparece assim:

```xml
xmlns="..."
```

Observe que não existe um nome depois de `xmlns`.

Esse é o namespace padrão.

Por isso, podemos escrever diretamente:

```xml
<ContentPage>
```

em vez de:

```xml
<meuComponente:ContentPage>
```

O namespace padrão permite utilizar os componentes diretamente pelo nome.

---

# 23. Namespace com nome

Também podemos criar um namespace com um nome:

```xml
xmlns:meuComponente="..."
```

Nesse caso:

```text
xmlns
```

indica o namespace.

```text
meuComponente
```

é o nome/prefixo escolhido.

Depois, os componentes podem ser acessados utilizando esse prefixo.

Por exemplo:

```xml
<meuComponente:ContentPage>
```

e:

```xml
<meuComponente:Label />
```

A aula demonstra que, se o namespace principal receber um nome, os componentes precisam utilizar esse prefixo para serem reconhecidos.

---

# 24. Por que utilizar um prefixo?

O prefixo funciona como uma espécie de identificação para aquele namespace.

Por exemplo:

```xml
xmlns:controles="..."
```

Depois podemos escrever:

```xml
<controles:MeuBotao />
```

O trecho:

```text
controles:
```

identifica o namespace.

E:

```text
MeuBotao
```

identifica o componente.

Podemos visualizar:

```text
controles:MeuBotao
   │          │
   │          └── Componente
   │
   └── Namespace/prefixo
```

---

# 25. Namespace `x`

Na `ContentPage`, também encontramos outro namespace:

```xml
xmlns:x="..."
```

Esse namespace é utilizado através do prefixo:

```text
x:
```

Ele aparece, por exemplo, em:

```xml
x:Class="..."
```

Nesse caso, `x:Class` não é um componente.

É um **atributo associado ao namespace `x`**.

---

# 26. O que significa `x:Class`?

O atributo:

```xml
x:Class="..."
```

indica qual é a classe C# associada àquela página.

Por exemplo:

```xml
x:Class="MeuProjeto.MainPage"
```

Podemos interpretar:

```text
XAML
 ↓
MainPage.xaml
 ↓
x:Class
 ↓
MeuProjeto.MainPage
 ↓
MainPage.xaml.cs
```

Ou seja, o XAML sabe qual é a classe C# que está por trás daquela tela.

Essa classe é o chamado **code-behind**.

A aula explica justamente que `x:Class` indica a classe que está por trás da tela.

---

# 27. Diferença entre `Title` e `x:Class`

É importante não confundir:

```xml
Title="MainPage"
```

com:

```xml
x:Class="MeuProjeto.MainPage"
```

Eles possuem funções diferentes.

### `Title`

É uma propriedade da `ContentPage`.

Serve para definir o título da página.

### `x:Class`

Pertence ao namespace `x`.

Indica qual classe C# está associada ao XAML.

Podemos resumir:

```text
Title
 ↓
Título da página

x:Class
 ↓
Classe C# associada
```

---

# 28. A propriedade `Title`

A `ContentPage` possui uma propriedade chamada:

```xml
Title="MainPage"
```

Essa propriedade representa o título da tela.

Porém, o título não necessariamente aparece diretamente no conteúdo da `ContentPage`.

Ele será visualizado quando existir uma estrutura de interface que apresente um cabeçalho.

Por exemplo, em uma estrutura de navegação, o título pode aparecer na barra superior.

---

# 29. Title e NavigationPage

Quando existe uma estrutura como uma `NavigationPage`, pode existir um cabeçalho na parte superior.

Visualmente:

```text
┌──────────────────────────────┐
│ ← MainPage                   │
├──────────────────────────────┤
│                              │
│       Conteúdo               │
│                              │
└──────────────────────────────┘
```

O texto:

```text
MainPage
```

pode vir da propriedade:

```xml
Title="MainPage"
```

Se alterarmos:

```xml
Title="Número da Sorte"
```

o título apresentado no cabeçalho será alterado para:

```text
Número da Sorte
```

A aula explica que essa propriedade ganha importância quando existe uma estrutura que apresenta o cabeçalho.

---

# 30. ContentPage como área de conteúdo

Depois de analisar a estrutura da página, podemos voltar ao conceito principal.

A `ContentPage` é a área onde colocamos os componentes que irão interagir com o usuário.

Por exemplo:

```text
ContentPage
│
└── VerticalStackLayout
    │
    ├── Label
    ├── Entry
    └── Button
```

Esses componentes formam o conteúdo apresentado ao usuário.

A aula reforça que as outras estruturas de navegação precisam trabalhar com páginas que apresentem conteúdo, e a `ContentPage` cumpre justamente esse papel.

---

# 31. Estrutura completa simplificada

Podemos imaginar uma `MainPage.xaml` simplificada:

```xml
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuProjeto.MainPage"
    Title="MainPage">

    <VerticalStackLayout>

        <Label
            Text="Número da Sorte" />

        <Button
            Text="Gerar número" />

    </VerticalStackLayout>

</ContentPage>
```

Agora podemos identificar cada parte.

---

# 32. Analisando a estrutura linha por linha

### Declaração XML

```xml
<?xml version="1.0" encoding="utf-8" ?>
```

Define informações do documento XML.

---

### ContentPage

```xml
<ContentPage>
```

Define a página de conteúdo.

---

### Namespace principal

```xml
xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
```

Define o namespace padrão utilizado pelos componentes do .NET MAUI.

Por estar sem um prefixo depois de `xmlns`, os componentes podem ser utilizados diretamente.

---

### Namespace `x`

```xml
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
```

Declara o namespace que será utilizado através do prefixo `x`.

Por isso podemos escrever:

```xml
x:Class
```

---

### `x:Class`

```xml
x:Class="MeuProjeto.MainPage"
```

Relaciona o arquivo XAML com a classe C# correspondente.

---

### `Title`

```xml
Title="MainPage"
```

Define o título da página.

---

### Layout

```xml
<VerticalStackLayout>
```

Organiza os componentes verticalmente.

---

### Label

```xml
<Label Text="Número da Sorte" />
```

Apresenta um texto.

---

### Button

```xml
<Button Text="Gerar número" />
```

Apresenta um botão.

---

# 33. Relação entre os arquivos

Podemos visualizar a relação entre os arquivos dessa maneira:

```text
MainPage.xaml
│
├── ContentPage
├── Layout
├── Label
└── Button
        │
        ↓
Interface
```

E:

```text
MainPage.xaml.cs
│
├── Classe MainPage
├── Métodos
├── Eventos
└── Lógica
```

Os dois arquivos trabalham juntos para formar a página.

---

# 34. Execução do projeto

Depois de realizar as alterações, o professor executa o projeto para verificar se a estrutura continua funcionando.

Mesmo depois de remover e recriar elementos, o projeto é compilado e executado normalmente.

O resultado apresentado é uma `ContentPage` simples.

Visualmente, podemos imaginar:

```text
┌──────────────────────────────┐
│                              │
│                              │
│       Conteúdo da página     │
│                              │
│                              │
└──────────────────────────────┘
```

Essa área representa o espaço onde os componentes da página são apresentados.

---

# 35. Principais conceitos aprendidos

|Conceito|Explicação|
|---|---|
|`ContentPage`|Página utilizada para apresentar conteúdo|
|XAML|Estrutura declarativa utilizada para construir a interface|
|Tag|Representa um componente|
|Atributo|Define uma característica/configuração do componente|
|`xmlns`|Declara um namespace|
|Namespace|Identifica de onde vêm componentes e recursos|
|Prefixo|Nome utilizado para identificar um namespace|
|`xmlns:x`|Declara o namespace utilizado pelo prefixo `x`|
|`x:Class`|Indica a classe C# associada ao XAML|
|`Title`|Define o título da página|
|Code-behind|Arquivo C# associado ao arquivo XAML|
|`F12`|Permite navegar até a definição de uma classe no Visual Studio|
|`MainPage.xaml`|Arquivo responsável pela interface|
|`MainPage.xaml.cs`|Arquivo responsável pela lógica da página|

---

# 36. Diferença entre os principais elementos

É importante memorizar a diferença entre eles:

```text
TAG
↓
Representa o componente

ATRIBUTO
↓
Configura o componente

NAMESPACE
↓
Identifica/importa componentes e recursos

x:Class
↓
Liga o XAML à classe C#

Title
↓
Define o título da página
```

---

# 37. Estrutura mental para entender um XAML

Quando encontrar um arquivo XAML, podemos analisá-lo de fora para dentro:

```text
1. Documento XML
       ↓
2. Namespace
       ↓
3. Página
       ↓
4. Atributos da página
       ↓
5. Layout
       ↓
6. Componentes
       ↓
7. Atributos dos componentes
```

Por exemplo:

```text
ContentPage
│
├── xmlns
├── xmlns:x
├── x:Class
├── Title
│
└── VerticalStackLayout
    │
    ├── Label
    │   └── Text
    │
    └── Button
        └── Text
```

Essa forma de pensar facilita bastante a leitura de XAML.

---

# 38. Conclusão

Nesta aula, foi criado um novo projeto para colocar em prática o conceito de `ContentPage`.

Além da criação da página, a aula serviu como uma revisão da estrutura do XAML.

Foi possível perceber que uma `ContentPage` é representada por uma tag e que os componentes utilizados dentro dela também são representações de classes do .NET MAUI.

Os atributos são utilizados para configurar características dos componentes, enquanto os namespaces permitem identificar e carregar componentes, bibliotecas e recursos.

Também foi apresentado o `x:Class`, que faz a ligação entre o arquivo XAML e a classe C# responsável pelo code-behind.

Outro ponto importante foi a propriedade `Title`, que representa o título da página e pode ser exibida em estruturas que possuem um cabeçalho, como uma estrutura de navegação.

A estrutura geral pode ser resumida assim:

```text
.NET MAUI
│
├── XAML
│   │
│   ├── ContentPage
│   │
│   ├── Tags
│   │
│   ├── Atributos
│   │
│   ├── Namespaces
│   │
│   └── Componentes
│
└── C#
    │
    └── Code-behind
        │
        └── Lógica da página
```

O principal aprendizado da aula é entender que o **XAML não é apenas um arquivo de configuração visual**. Ele representa uma estrutura hierárquica de objetos e componentes que possuem correspondência com classes e propriedades no C#.

Dessa forma, ao olhar para:

```xml
<ContentPage>
```

podemos pensar:

```text
ContentPage
↓
Componente
↓
Classe do .NET MAUI
↓
Possui propriedades e métodos
```

E ao olhar para:

```xml
Title="MainPage"
```

podemos pensar:

```text
Title
↓
Atributo XAML
↓
Propriedade da ContentPage
```

Essa compreensão será importante para as próximas aulas, principalmente quando forem trabalhadas outras páginas, navegação e componentes personalizados.