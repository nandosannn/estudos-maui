# .NET MAUI — Criando o Menu Dinamicamente com C#

## 1. Objetivo da aula

O objetivo principal desta aula é substituir as `Label`s estáticas do menu por elementos criados **dinamicamente através do C#**.

Anteriormente, o menu possuía informações escritas diretamente no XAML:

```xml
<Label Text="Layouts" />
<Label Text="StackLayout" />
<Label Text="Organização sequencial dos elementos." />
```

Agora essas informações serão obtidas do:

```text
CategoryRepository
        ↓
Categories
        ↓
Components
        ↓
C#
        ↓
Labels
        ↓
Menu
```

Assim, o menu passa a ser gerado automaticamente de acordo com os dados cadastrados no `Repository`.

---

# 2. Por que criar os elementos pelo C#?

O XAML é utilizado para definir a interface visual, mas os elementos também podem ser criados e manipulados através do C#.

Por exemplo, uma `Label` pode ser criada diretamente no código:

```csharp
Label label = new Label();
```

E suas propriedades podem ser configuradas:

```csharp
label.Text = "StackLayout";
```

Depois, ela pode ser adicionada a um elemento da interface.

Isso permite criar interfaces **dinamicamente durante a execução do aplicativo**.

---

# 3. `InitializeComponent()`

O projeto utiliza XAML para definir a interface.

Quando o XAML é carregado, o método:

```csharp
InitializeComponent();
```

é responsável por inicializar os elementos definidos no XAML.

Porém, depois dessa inicialização, também podemos acessar esses elementos pelo C# e modificá-los ou adicionar novos componentes.

Exemplo:

```text
XAML
 ↓
InitializeComponent()
 ↓
Elementos da interface
 ↓
C# pode acessar e modificar
```

---

# 4. Criação do `MenuContainer`

As `Label`s que existiam anteriormente foram removidas.

No lugar delas, foi criado um `VerticalStackLayout`:

```xml
<VerticalStackLayout
    x:Name="MenuContainer">
</VerticalStackLayout>
```

O `x:Name` é importante porque permite acessar esse componente diretamente pelo Code Behind.

No C# podemos utilizar:

```csharp
MenuContainer
```

Assim, conseguimos adicionar novos elementos dinamicamente.

---

# 5. O que é `x:Name`?

O atributo:

```xml
x:Name="MenuContainer"
```

define um nome para o elemento XAML.

Esse nome permite acessá-lo no C#.

Exemplo:

```xml
<VerticalStackLayout
    x:Name="MenuContainer" />
```

No Code Behind:

```csharp
MenuContainer.Children.Add(label);
```

Podemos pensar assim:

```text
XAML
 ↓
x:Name
 ↓
Variável acessível no C#
```

---

# 6. Obtendo as categorias do Repository

No construtor do `Menu`, o `CategoryRepository` é instanciado:

```csharp
var repository = new CategoryRepository();
```

Depois são obtidas as categorias:

```csharp
var categories = repository.GetCategories();
```

O resultado é uma:

```csharp
List<Category>
```

A estrutura fica:

```text
CategoryRepository
       ↓
GetCategories()
       ↓
List<Category>
       ↓
categories
```

---

# 7. Percorrendo as categorias

Para percorrer todas as categorias, foi utilizado um `foreach`:

```csharp
foreach (var category in categories)
{
    // Criar elementos da categoria
}
```

Isso significa:

> Para cada categoria existente na lista, execute o código.

Por exemplo:

```text
categories
│
├── Layouts
├── Formulários
└── Outros
```

O `foreach` percorrerá:

```text
1ª iteração → Layouts
2ª iteração → Formulários
3ª iteração → Outros
```

---

# 8. Criando a Label da categoria

Para cada categoria, é criada uma nova `Label`:

```csharp
var lblCategory = new Label
{
    Text = category.Name
};
```

A propriedade:

```csharp
category.Name
```

vem diretamente do objeto `Category`.

Por exemplo:

```text
Category.Name
      ↓
"Layouts"
      ↓
Label.Text
      ↓
"Layouts"
```

Assim, o texto não fica mais fixo no XAML.

---

# 9. Adicionando a categoria ao menu

Depois de criar a `Label`, ela é adicionada ao `MenuContainer`:

```csharp
MenuContainer.Children.Add(lblCategory);
```

A estrutura fica:

```text
MenuContainer
    │
    └── Label
         └── "Layouts"
```

---

# 10. Percorrendo os componentes

Cada categoria possui uma lista de componentes:

```csharp
category.Components
```

Por isso, dentro do primeiro `foreach`, é criado um segundo:

```csharp
foreach (var component in category.Components)
{
    // Criar elementos do componente
}
```

Temos então um `foreach` dentro de outro `foreach`.

### Estrutura

```text
foreach Category
    ↓
    foreach Component
        ↓
        Criar Labels
```

---

# 11. Dois níveis de repetição

Esse conceito é importante para entender a estrutura dos dados.

```text
Categorias
│
├── Layouts
│   ├── StackLayout
│   ├── Grid
│   └── FlexLayout
│
├── Formulários
│   ├── Entry
│   ├── Editor
│   └── Picker
│
└── Outros
    ├── Button
    └── Image
```

O primeiro `foreach` percorre as categorias.

O segundo `foreach` percorre os componentes pertencentes à categoria atual.

---

# 12. Criando a Label do título

Para cada componente é criada uma `Label` para seu título:

```csharp
var lblComponentTitle = new Label
{
    Text = component.Title
};
```

O texto vem de:

```csharp
component.Title
```

Por exemplo:

```text
Component.Title
       ↓
"StackLayout"
       ↓
Label.Text
```

---

# 13. Criando a Label da descrição

Também é criada uma `Label` para apresentar a descrição:

```csharp
var lblComponentDescription = new Label
{
    Text = component.Description
};
```

Por exemplo:

```text
Component.Description
        ↓
"Organização sequencial dos elementos."
        ↓
Label.Text
```

---

# 14. Adicionando as Labels ao `MenuContainer`

Depois de criar as duas Labels, elas são adicionadas ao `VerticalStackLayout`:

```csharp
MenuContainer.Children.Add(lblComponentTitle);

MenuContainer.Children.Add(lblComponentDescription);
```

A estrutura visual fica:

```text
MenuContainer
│
├── Layouts
│
├── StackLayout
├── Organização sequencial dos elementos.
│
├── Grid
├── Organização em linhas e colunas.
│
└── ...
```

---

# 15. A propriedade `Children`

Um dos principais conceitos apresentados na aula é a propriedade:

```csharp
Children
```

Elementos como `VerticalStackLayout` podem conter vários elementos filhos.

Por exemplo:

```text
VerticalStackLayout
│
├── Label
├── Label
├── Button
├── Image
└── ...
```

Esses elementos ficam armazenados na coleção:

```csharp
Children
```

---

# 16. Adicionando elementos através de `Children`

Para adicionar um elemento:

```csharp
MenuContainer.Children.Add(label);
```

Podemos interpretar:

```text
MenuContainer
      ↓
Children
      ↓
Add()
      ↓
Novo elemento
```

Exemplo:

```csharp
var label = new Label
{
    Text = "Olá"
};

MenuContainer.Children.Add(label);
```

Resultado:

```text
VerticalStackLayout
└── Label
    └── Olá
```

---

# 17. `Children` é uma coleção

A propriedade `Children` representa uma coleção de elementos filhos.

Por isso, podemos adicionar vários elementos:

```csharp
MenuContainer.Children.Add(label1);
MenuContainer.Children.Add(label2);
MenuContainer.Children.Add(label3);
```

Ou acessar elementos existentes através de índices:

```csharp
MenuContainer.Children[0]
MenuContainer.Children[1]
MenuContainer.Children[2]
```

O índice começa em:

```text
0
```

Então:

```text
Children[0] → primeiro elemento
Children[1] → segundo elemento
Children[2] → terceiro elemento
```

---

# 18. Estrutura final do código

A lógica desenvolvida pode ser representada assim:

```csharp
public Menu()
{
    InitializeComponent();

    var repository = new CategoryRepository();

    var categories = repository.GetCategories();

    foreach (var category in categories)
    {
        var lblCategory = new Label
        {
            Text = category.Name
        };

        MenuContainer.Children.Add(lblCategory);

        foreach (var component in category.Components)
        {
            var lblComponentTitle = new Label
            {
                Text = component.Title
            };

            var lblComponentDescription = new Label
            {
                Text = component.Description
            };

            MenuContainer.Children.Add(lblComponentTitle);
            MenuContainer.Children.Add(lblComponentDescription);
        }
    }
}
```

---

# 19. Funcionamento do código

O fluxo completo é:

```text
Menu é criado
     ↓
InitializeComponent()
     ↓
Cria CategoryRepository
     ↓
GetCategories()
     ↓
Obtém categorias
     ↓
foreach categoria
     ↓
Cria Label da categoria
     ↓
Adiciona ao MenuContainer
     ↓
foreach componente
     ↓
Cria Label do título
     ↓
Cria Label da descrição
     ↓
Adiciona as Labels ao MenuContainer
```

---

# 20. Resultado esperado

Se o Repository possuir:

```text
Categoria:
    Layouts

Componente:
    StackLayout
    "Organização sequencial dos elementos."
```

O menu será montado aproximadamente assim:

```text
MAUI Gallery

Início
Extra
Créditos

Layouts

StackLayout
Organização sequencial dos elementos.
```

Se posteriormente adicionarmos:

```text
Layouts
├── StackLayout
├── Grid
└── FlexLayout
```

o menu poderá apresentar automaticamente:

```text
Layouts

StackLayout
Organização sequencial dos elementos.

Grid
Organização dos elementos em linhas e colunas.

FlexLayout
Organização flexível dos elementos.
```

Sem precisar criar manualmente cada `Label` no XAML.

---

# 21. XAML x C#

Uma ideia importante da aula é que podemos trabalhar a interface tanto no XAML quanto no C#.

|XAML|C#|
|---|---|
|Define elementos visualmente|Cria elementos por código|
|Mais declarativo|Mais programático|
|Ideal para estrutura inicial|Ideal para criação dinâmica|
|`Text="StackLayout"`|`Text = component.Title`|
|`<Label />`|`new Label()`|
|`<VerticalStackLayout>`|`new VerticalStackLayout()`|

### Exemplo

**XAML:**

```xml
<Label Text="StackLayout" />
```

**C#:**

```csharp
var label = new Label
{
    Text = "StackLayout"
};
```

---

# 22. Abordagem estática x dinâmica

### Antes — estática

```text
XAML
 ↓
Label fixa
 ↓
"Layouts"

Label fixa
 ↓
"StackLayout"

Label fixa
 ↓
"Descrição"
```

### Agora — dinâmica

```text
Repository
 ↓
Category
 ↓
Component
 ↓
C#
 ↓
new Label()
 ↓
MenuContainer.Children.Add()
 ↓
Interface
```

Essa mudança torna o projeto muito mais flexível.

---

# 23. Observação sobre boas práticas

Na aula, o `CategoryRepository` é instanciado diretamente:

```csharp
var repository = new CategoryRepository();
```

Isso foi feito propositalmente para manter o projeto simples neste momento.

O .NET MAUI possui um sistema de **injeção de dependência**, que poderá ser utilizado posteriormente.

A ideia apresentada pelo professor é evoluir o projeto gradualmente:

```text
Projeto inicial
      ↓
Código simples
      ↓
Mais componentes
      ↓
Melhores práticas
      ↓
Injeção de dependência
      ↓
Arquitetura mais organizada
```

---

# 24. Resumo dos principais conceitos

|Conceito|Função|
|---|---|
|`Code Behind`|Permite manipular a interface através do C#|
|`InitializeComponent()`|Inicializa os elementos definidos no XAML|
|`x:Name`|Permite acessar um elemento XAML pelo C#|
|`MenuContainer`|`VerticalStackLayout` utilizado como container do menu|
|`Children`|Coleção que armazena os elementos filhos|
|`Children.Add()`|Adiciona um elemento ao container|
|`foreach`|Percorre uma coleção|
|`categories`|Lista de categorias|
|`category.Components`|Lista de componentes da categoria|
|`new Label()`|Cria uma Label através do C#|
|`component.Title`|Obtém o título do componente|
|`component.Description`|Obtém a descrição do componente|
|`CategoryRepository`|Fornece os dados das categorias|
|`GetCategories()`|Retorna a lista de categorias|

---

# 25. Conceito principal para memorizar

A grande ideia desta aula é:

> **Elementos da interface do .NET MAUI também podem ser criados, configurados e adicionados dinamicamente através do C#.**

O exemplo principal é:

```csharp
var label = new Label
{
    Text = component.Title
};

MenuContainer.Children.Add(label);
```

Ou seja:

```text
Criar componente
      ↓
Configurar propriedades
      ↓
Adicionar ao container
      ↓
Componente aparece na interface
```

E, utilizando o `Repository`:

```text
Repository
     ↓
Dados
     ↓
foreach
     ↓
Criação das Labels
     ↓
Children.Add()
     ↓
Menu dinâmico
```

Essa estrutura será a base para a próxima etapa, na qual o menu poderá receber **estilos, comportamentos e navegação**, permitindo que o usuário clique em um componente e seja levado para sua página de demonstração.