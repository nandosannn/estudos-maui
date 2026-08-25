# .NET MAUI — Organização de Categorias e Componentes

## 1. Objetivo da aula

O **MAUI Gallery** será uma aplicação utilizada como uma galeria de demonstração dos componentes disponíveis no .NET MAUI.

Para organizar essa galeria, o aplicativo terá:

- Página inicial (**Home/Início**);
    
- Página **Extra**, com dicas e links;
    
- Página de **Créditos/Sobre**;
    
- Categorias de componentes;
    
- Componentes dentro de cada categoria;
    
- Uma página específica para demonstrar cada componente.
    

A estrutura conceitual será:

```text
MAUI Gallery
│
├── Início
├── Extra
├── Créditos / Sobre
│
└── Categorias
    ├── Layouts
    │   ├── StackLayout
    │   ├── Grid
    │   └── ...
    │
    ├── Formulários
    │   ├── Entry
    │   ├── Editor
    │   └── ...
    │
    └── Outros
        ├── Button
        ├── Image
        └── ...
```

---

# 2. Problema da abordagem inicial

Inicialmente, seria possível criar manualmente várias `Label`s:

```xml
<Label Text="Layouts" />

<Label Text="StackLayout" />

<Label Text="Organização sequencial dos elementos." />
```

E repetir isso para todos os componentes.

Porém, essa abordagem apresenta um problema:

- muito código repetido;
    
- difícil manutenção;
    
- difícil adicionar novos componentes;
    
- difícil alterar informações;
    
- estrutura pouco escalável.
    

Por isso, a aula propõe transformar essas informações em **objetos C#**.

---

# 3. Organização baseada em dados

Em vez de criar cada componente diretamente no XAML, serão criadas classes que representam os dados.

A estrutura será:

```text
Categoria
   │
   ├── Nome
   ├── Descrição
   │
   └── Componentes
          │
          ├── Título
          ├── Descrição
          └── Página
```

Isso permite que o menu seja posteriormente construído dinamicamente.

---

# 4. Criação da pasta `Models`

Foi criada uma pasta chamada:

```text
Models
```

Essa pasta será responsável por armazenar as classes que representam os dados da aplicação.

Estrutura:

```text
Models
│
├── Category.cs
└── Component.cs
```

---

# 5. Classe `Category`

A classe `Category` representa uma **categoria de componentes**.

Exemplo:

```csharp
public class Category
{
    public string Name { get; set; }

    public string Description { get; set; }

    public List<Component> Components { get; set; }
}
```

### Propriedades

|Propriedade|Tipo|Função|
|---|---|---|
|`Name`|`string`|Nome da categoria|
|`Description`|`string`|Descrição da categoria|
|`Components`|`List<Component>`|Componentes pertencentes à categoria|

---

# 6. Relação entre `Category` e `Component`

Uma categoria pode possuir vários componentes.

Por isso:

```csharp
public List<Component> Components { get; set; }
```

representa uma relação:

```text
Category
   │
   └── Components
          ├── Component
          ├── Component
          └── Component
```

Por exemplo:

```text
Layouts
│
├── StackLayout
├── Grid
├── FlexLayout
└── HorizontalStackLayout
```

---

# 7. Classe `Component`

A classe `Component` representa um componente que será apresentado na galeria.

Ela possui três informações principais:

```csharp
public class Component
{
    public string Title { get; set; }

    public string Description { get; set; }

    public Page Page { get; set; }
}
```

### Propriedades

|Propriedade|Tipo|Função|
|---|---|---|
|`Title`|`string`|Nome/título do componente|
|`Description`|`string`|Descrição do componente|
|`Page`|`Page`|Página que será aberta ao selecionar o componente|

---

# 8. Propriedade `Page`

A propriedade:

```csharp
public Page Page { get; set; }
```

é um dos conceitos mais importantes apresentados na aula.

`Page` é uma classe do .NET MAUI da qual diferentes tipos de páginas herdam.

Por exemplo:

```text
Page
│
├── ContentPage
├── NavigationPage
├── FlyoutPage
├── TabbedPage
└── ...
```

Portanto, uma propriedade do tipo `Page` pode receber diferentes tipos de páginas compatíveis.

No projeto, essa propriedade será utilizada para indicar:

> "Qual página deve ser aberta quando o usuário selecionar este componente?"

---

# 9. Exemplo de um componente

O componente `StackLayout` poderá ser representado por:

```csharp
new Component
{
    Title = "StackLayout",
    Description = "Organização sequencial dos elementos.",
    Page = new StackLayoutPage()
}
```

A ideia é:

```text
StackLayout
     │
     ├── Título
     ├── Descrição
     │
     └── Página
          ↓
    StackLayoutPage
```

---

# 10. Criação da página do componente

Foi criada uma nova organização dentro de `Views`:

```text
Views
│
├── MainPage.xaml
├── Menu.xaml
│
└── Layouts
    └── StackLayoutPage.xaml
```

A página:

```text
StackLayoutPage
```

será utilizada para explicar e demonstrar o funcionamento do `StackLayout`.

Isso permite separar:

- a página que lista os componentes;
    
- da página que demonstra cada componente.
    

---

# 11. Criação da pasta `Repository`

Além dos `Models`, foi criada uma pasta:

```text
Repository
```

Ela será responsável por fornecer as categorias e componentes utilizados pelo aplicativo.

Estrutura:

```text
Repository
└── CategoryRepository.cs
```

---

# 12. `CategoryRepository`

O `CategoryRepository` funciona como uma espécie de **fonte de dados** para o aplicativo.

Neste projeto, não será utilizado um banco de dados para armazenar as categorias e componentes.

Em vez disso, os dados serão definidos diretamente no código.

A ideia é:

```text
CategoryRepository
        ↓
Lista de categorias
        ↓
Categorias
        ↓
Componentes
```

---

# 13. Método `GetCategories()`

Foi criado um método responsável por retornar todas as categorias:

```csharp
public List<Category> GetCategories()
{
    ...
}
```

O retorno é:

```csharp
List<Category>
```

Ou seja, o método fornece uma lista de objetos `Category`.

---

# 14. Exemplo de implementação

A estrutura criada na aula pode ser representada da seguinte maneira:

```csharp
public List<Category> GetCategories()
{
    return new List<Category>
    {
        new Category
        {
            Name = "Layouts",

            Components = new List<Component>
            {
                new Component
                {
                    Title = "StackLayout",
                    Description = "Organização sequencial dos elementos.",
                    Page = new StackLayoutPage()
                }
            }
        }
    };
}
```

A estrutura dos dados fica:

```text
Lista de Categorias
│
└── Layouts
    │
    └── Lista de Componentes
        │
        └── StackLayout
            ├── Title
            ├── Description
            └── Page
```

---

# 15. Por que utilizar um Repository?

O `Repository` centraliza os dados utilizados pelo aplicativo.

Em vez de colocar as informações diretamente no `Menu`, podemos fazer:

```text
Menu
  ↓
Repository
  ↓
Categories
  ↓
Components
```

Isso deixa o `Menu` responsável principalmente pela **apresentação**, enquanto o `Repository` fica responsável pelos **dados**.

---

# 16. Separação de responsabilidades

A organização criada começa a separar as responsabilidades do projeto.

|Local|Responsabilidade|
|---|---|
|`Views`|Interface e páginas|
|`Models`|Representação dos dados|
|`Repository`|Fornecimento dos dados|
|`Menu`|Apresentação e interação com o menu|
|`Category`|Representação de uma categoria|
|`Component`|Representação de um componente|

Essa separação facilita a evolução do projeto.

---

# 17. Estrutura atual do projeto

Ao final da aula, a estrutura começa a ficar assim:

```text
MAUI Gallery
│
├── Models
│   ├── Category.cs
│   └── Component.cs
│
├── Repository
│   └── CategoryRepository.cs
│
├── Views
│   ├── MainPage.xaml
│   ├── Menu.xaml
│   │
│   └── Layouts
│       └── StackLayoutPage.xaml
│
└── AppFlyOut.xaml
```

---

# 18. Fluxo dos dados

O funcionamento planejado será:

```text
CategoryRepository
        ↓
GetCategories()
        ↓
List<Category>
        ↓
Category
        ↓
List<Component>
        ↓
Component
        ↓
Usuário seleciona componente
        ↓
Component.Page
        ↓
Página de demonstração
```

Por exemplo:

```text
CategoryRepository
        ↓
Layouts
        ↓
StackLayout
        ↓
StackLayoutPage
```

---

# 19. Vantagem da estrutura

A principal vantagem é que podemos adicionar novos componentes sem precisar criar manualmente toda a estrutura visual do menu.

Por exemplo, para adicionar `Grid`:

```csharp
new Component
{
    Title = "Grid",
    Description = "Organização de elementos em linhas e colunas.",
    Page = new GridPage()
}
```

Depois, o sistema poderá utilizar essas informações para gerar o menu automaticamente.

Assim, adicionar componentes passa a ser muito mais simples.

---

# 20. Resumo dos principais conceitos

|Conceito|Função|
|---|---|
|**Models**|Armazena as classes que representam os dados|
|**Category**|Representa uma categoria|
|**Component**|Representa um componente do MAUI|
|**List**|Armazena vários componentes dentro de uma categoria|
|**Page**|Representa uma página do .NET MAUI|
|**Component.Page**|Indica qual página deve ser aberta|
|**Repository**|Fornece os dados para a aplicação|
|**CategoryRepository**|Fornece as categorias e seus componentes|
|**GetCategories()**|Retorna a lista de categorias|
|**Views**|Armazena as páginas da aplicação|
|**StackLayoutPage**|Página responsável por demonstrar o `StackLayout`|

---

# 21. Conceito mais importante da aula

A grande mudança desta aula é passar de uma interface **fixa** para uma interface baseada em **dados estruturados**.

### Antes

```text
XAML
 ↓
Label "Layouts"
 ↓
Label "StackLayout"
 ↓
Label "Descrição"
```

### Depois

```text
Repository
 ↓
Category
 ↓
Component
 ↓
Menu
 ↓
Interface dinâmica
```

Isso torna o MAUI Gallery mais organizado, reutilizável e escalável.

---

## Estrutura para memorizar

```text
CATEGORY
│
├── Name
├── Description
│
└── Components
      │
      └── COMPONENT
            ├── Title
            ├── Description
            └── Page
```

E os dados serão fornecidos por:

```text
CategoryRepository
        ↓
GetCategories()
        ↓
List<Category>
```

**Próxima etapa:** adaptar o `Menu` para consumir essa lista de categorias e componentes e gerar a interface dinamicamente, em vez de criar cada `Label` manualmente.