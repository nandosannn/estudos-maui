# TabbedPage no .NET MAUI

## 1. O que é a TabbedPage?

A `TabbedPage` é um tipo de página do .NET MAUI utilizado para criar uma interface baseada em **abas**.

A ideia é permitir que o usuário navegue entre diferentes páginas através de abas.

Um exemplo visual seria:

```text
+------------------------------------------+
| Página 1 | Página 2 | Página 3           |
+------------------------------------------+
|                                          |
|           Conteúdo da página             |
|                                          |
|                                          |
+------------------------------------------+
```

Cada aba representa uma página diferente.

Por exemplo:

```text
Aba 1 → Page1
Aba 2 → Page2
Aba 3 → Page3
```

Quando o usuário seleciona uma aba, o conteúdo correspondente é apresentado automaticamente.

---

# 2. Comparação com o FlyoutPage

Anteriormente, estudamos o `FlyoutPage`.

O `FlyoutPage` utiliza um **menu lateral**:

```text
FlyoutPage
│
├── Flyout
│   ├── Página 1
│   ├── Página 2
│   └── Página 3
│
└── Detail
    └── Página atual
```

Já a `TabbedPage` utiliza **abas**:

```text
TabbedPage
│
├── Aba 1 → Página 1
├── Aba 2 → Página 2
└── Aba 3 → Página 3
```

A principal diferença está na forma como o usuário navega.

| Página           | Forma de navegação    |
| ---------------- | --------------------- |
| `ContentPage`    | Apresenta conteúdo    |
| `NavigationPage` | Navegação hierárquica |
| `FlyoutPage`     | Menu lateral          |
| `TabbedPage`     | Abas                  |

---

# 3. Criando um projeto para testar a TabbedPage

Na aula, é criado um novo projeto para testar esse tipo de página.

Depois da criação do projeto, a estrutura padrão é limpa para que possamos construir a aplicação utilizando a `TabbedPage`.

A ideia é criar três páginas de conteúdo:

```text
Page1
Page2
Page3
```

Cada uma dessas páginas será utilizada como uma aba.

---

# 4. Criando as páginas

Primeiro criamos a `Page1`.

Depois criamos:

```text
Page2
Page3
```

Ao final, teremos:

```text
Projeto
│
├── Page1.xaml
├── Page1.xaml.cs
│
├── Page2.xaml
├── Page2.xaml.cs
│
└── Page3.xaml
    └── Page3.xaml.cs
```

Cada página terá seu próprio conteúdo.

---

# 5. Identificando cada página

Para facilitar a visualização durante os testes, podemos colocar um texto diferente em cada página.

### Page1

```xml
<Label
    Text="Página 1"
    FontSize="48" />
```

### Page2

```xml
<Label
    Text="Página 2"
    FontSize="48" />
```

### Page3

```xml
<Label
    Text="Página 3"
    FontSize="48" />
```

Assim conseguimos identificar facilmente qual página está sendo apresentada.

---

# 6. A TabbedPage como estrutura de organização

Um ponto muito importante apresentado na aula é que a `TabbedPage` não precisa necessariamente conter diretamente todo o conteúdo da aplicação.

Ela pode funcionar como uma estrutura responsável por **organizar outras páginas**.

Podemos pensar nela desta forma:

```text
TabbedPage
│
├── Page1
├── Page2
└── Page3
```

Cada página representa uma aba.

Isso é diferente de uma `ContentPage`, que normalmente é utilizada para construir diretamente uma tela.

---

# 7. Criando o arquivo de configuração das abas

Assim como o `FlyoutPage` possui uma estrutura responsável por organizar o menu e o `Detail`, a `TabbedPage` pode ter uma página responsável por definir quais páginas serão utilizadas como abas.

Podemos criar uma página chamada, por exemplo:

```text
TabbedPageMenu
```

A nomenclatura segue a mesma ideia utilizada anteriormente com:

```text
FlyoutPageMenu
```

A função dessa página será organizar as abas.

---

# 8. Alterando ContentPage para TabbedPage

Ao criar uma nova página pelo Visual Studio, ela pode ser criada inicialmente como uma `ContentPage`.

Porém, nesse caso, queremos utilizar uma `TabbedPage`.

Então precisamos alterar o elemento principal do XAML.

Em vez de:

```xml
<ContentPage>
```

utilizaremos:

```xml
<TabbedPage>
```

Da mesma forma, no arquivo `.xaml.cs`, a classe deverá herdar de `TabbedPage`.

Por exemplo:

```csharp
public partial class TabbedPageMenu : TabbedPage
{
    public TabbedPageMenu()
    {
        InitializeComponent();
    }
}
```

A partir desse momento, essa página deixa de ser uma página de conteúdo comum e passa a ser uma estrutura de abas.

---

# 9. Removendo o layout da ContentPage

Como não estamos mais criando uma `ContentPage` tradicional, não precisamos manter um:

```xml
<VerticalStackLayout>
```

ou outro layout para organizar o conteúdo diretamente.

A `TabbedPage` terá como responsabilidade organizar outras páginas.

Portanto, sua estrutura pode ser mais simples.

---

# 10. Importando as páginas

Para utilizar `Page1`, `Page2` e `Page3` dentro da `TabbedPage`, precisamos disponibilizar o namespace onde essas páginas estão localizadas.

Podemos fazer isso com:

```xml
xmlns:pages="clr-namespace:NomeDoProjeto"
```

Por exemplo, se o projeto se chama `AppTabbedPage`:

```xml
xmlns:pages="clr-namespace:AppTabbedPage"
```

Agora podemos utilizar as páginas através do namespace `pages`.

---

# 11. Adicionando as páginas como abas

Depois de importar o namespace, podemos adicionar as páginas:

```xml
<TabbedPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:pages="clr-namespace:AppTabbedPage"
    x:Class="AppTabbedPage.TabbedPageMenu">

    <pages:Page1 />

    <pages:Page2 />

    <pages:Page3 />

</TabbedPage>
```

Essa é a parte principal da configuração.

Estamos dizendo:

```text
TabbedPage
│
├── Page1
├── Page2
└── Page3
```

O .NET MAUI entende que cada uma dessas páginas representa uma aba.

---

# 12. Não precisamos programar a troca de abas

Essa é uma das principais diferenças entre a `TabbedPage` e o exemplo que fizemos com `FlyoutPage`.

No `FlyoutPage`, precisávamos criar eventos:

```csharp
Clicked
```

e alterar:

```csharp
flyoutPage.Detail
```

Por exemplo:

```csharp
flyoutPage.Detail = new Page2();
```

Na `TabbedPage`, não precisamos fazer isso manualmente.

Basta declarar as páginas:

```xml
<pages:Page1 />
<pages:Page2 />
<pages:Page3 />
```

A própria `TabbedPage` controla a navegação entre elas.

---

# 13. Como funciona a navegação

Se temos:

```xml
<TabbedPage>

    <pages:Page1 />

    <pages:Page2 />

    <pages:Page3 />

</TabbedPage>
```

o .NET MAUI cria automaticamente a estrutura de abas.

O usuário pode clicar em:

```text
Página 1
```

e verá:

```text
Conteúdo da Page1
```

Depois clicar em:

```text
Página 2
```

e verá:

```text
Conteúdo da Page2
```

E finalmente:

```text
Página 3
```

para visualizar:

```text
Conteúdo da Page3
```

Não precisamos criar manualmente os eventos de clique para fazer essa troca.

---

# 14. O título das abas

Um detalhe importante da aula é que o texto exibido nas abas pode ser obtido da propriedade:

```xml
Title
```

de cada página.

Por exemplo, na `Page1`:

```xml
<ContentPage
    Title="Página 1">
```

Na `Page2`:

```xml
<ContentPage
    Title="Página 2">
```

E na `Page3`:

```xml
<ContentPage
    Title="Página 3">
```

A `TabbedPage` utiliza essas informações para identificar as abas.

Podemos imaginar:

```text
+------------------------------------------------+
| Página 1 | Página 2 | Página 3                 |
+------------------------------------------------+
```

Esses textos podem ser alterados modificando o `Title` de cada página.

---

# 15. Exemplo completo

Podemos criar três páginas.

## Page1.xaml

```xml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppTabbedPage.Page1"
    Title="Página 1">

    <VerticalStackLayout
        Padding="15">

        <Label
            Text="Página 1"
            FontSize="48"
            HorizontalOptions="Center" />

    </VerticalStackLayout>

</ContentPage>
```

---

## Page2.xaml

```xml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppTabbedPage.Page2"
    Title="Página 2">

    <VerticalStackLayout
        Padding="15">

        <Label
            Text="Página 2"
            FontSize="48"
            HorizontalOptions="Center" />

    </VerticalStackLayout>

</ContentPage>
```

---

## Page3.xaml

```xml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppTabbedPage.Page3"
    Title="Página 3">

    <VerticalStackLayout
        Padding="15">

        <Label
            Text="Página 3"
            FontSize="48"
            HorizontalOptions="Center" />

    </VerticalStackLayout>

</ContentPage>
```

---

# 16. TabbedPageMenu.xaml

Agora criamos a estrutura responsável pelas abas:

```xml
<TabbedPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:pages="clr-namespace:AppTabbedPage"
    x:Class="AppTabbedPage.TabbedPageMenu">

    <pages:Page1 />

    <pages:Page2 />

    <pages:Page3 />

</TabbedPage>
```

---

# 17. TabbedPageMenu.xaml.cs

O Code Behind pode ficar:

```csharp
namespace AppTabbedPage;

public partial class TabbedPageMenu : TabbedPage
{
    public TabbedPageMenu()
    {
        InitializeComponent();
    }
}
```

Observe que agora a classe herda de:

```csharp
TabbedPage
```

e não de:

```csharp
ContentPage
```

Essa alteração é fundamental.

---

# 18. Definindo a página inicial

Por fim, precisamos informar ao aplicativo qual página deve ser carregada inicialmente.

No `App.xaml.cs`, podemos utilizar:

```csharp
public partial class App : Application
{
    public App()
    {
        InitializeComponent();

        MainPage = new TabbedPageMenu();
    }
}
```

Assim, quando o aplicativo iniciar:

```text
Aplicação
    ↓
TabbedPageMenu
    ↓
┌──────────┬──────────┬──────────┐
│ Página 1 │ Página 2 │ Página 3 │
└──────────┴──────────┴──────────┘
```

---

# 19. Fluxo completo da aplicação

O funcionamento pode ser resumido assim:

```text
App
 ↓
TabbedPageMenu
 ↓
TabbedPage
 ├── Page1
 ├── Page2
 └── Page3
```

Quando o usuário seleciona uma aba:

```text
Usuário clica na aba
        ↓
TabbedPage identifica a página
        ↓
Página selecionada é apresentada
```

Não precisamos criar:

```csharp
Clicked
```

nem:

```csharp
Detail = ...
```

para fazer a navegação básica entre as abas.

---

# 20. Diferença entre FlyoutPage e TabbedPage

Essa comparação é importante para entender quando utilizar cada uma.

|Característica|FlyoutPage|TabbedPage|
|---|---|---|
|Navegação principal|Menu lateral|Abas|
|Elemento principal|`Flyout` + `Detail`|Coleção de páginas|
|Troca de página|Pode exigir programação|Gerenciada pela própria página|
|Interface|Menu lateral|Abas|
|Boa utilização|Muitas funcionalidades|Poucos grupos de conteúdo relacionados|
|Usuário seleciona|Item do menu|Aba|
|Organização|Menu + conteúdo|Abas + conteúdo|

---

# 21. Exemplo de aplicação com TabbedPage

Imagine um aplicativo de música.

Podemos ter:

```text
┌──────────┬──────────┬──────────┐
│ Músicas  │ Artistas │ Álbuns   │
└──────────┴──────────┴──────────┘
```

Cada aba seria uma página:

```text
Músicas  → SongsPage
Artistas → ArtistsPage
Álbuns   → AlbumsPage
```

A configuração seria:

```xml
<TabbedPage>

    <pages:SongsPage />

    <pages:ArtistsPage />

    <pages:AlbumsPage />

</TabbedPage>
```

O usuário simplesmente troca de aba para navegar.

---

# 22. Quando utilizar TabbedPage?

A `TabbedPage` é interessante quando temos **poucas categorias principais de conteúdo** que precisam estar facilmente acessíveis.

Exemplos:

```text
WhatsApp
├── Conversas
├── Atualizações
└── Ligações
```

Ou:

```text
Aplicativo de música
├── Músicas
├── Artistas
└── Álbuns
```

Ou:

```text
Aplicativo de notícias
├── Notícias
├── Favoritos
└── Mais lidas
```

A ideia é que as opções principais estejam disponíveis diretamente nas abas.

---

# 23. Quando utilizar FlyoutPage?

O `FlyoutPage` costuma ser mais adequado quando temos muitas funcionalidades.

Por exemplo:

```text
☰ Menu

├── Início
├── Usuários
├── Produtos
├── Vendas
├── Relatórios
├── Configurações
├── Perfil
└── Sobre
```

Nesse cenário, colocar todas essas opções como abas poderia deixar a interface muito carregada.

O menu lateral consegue organizar uma quantidade maior de opções.

---

# 24. Conceitos principais da aula

|Conceito|Significado|
|---|---|
|`TabbedPage`|Página que organiza outras páginas em abas|
|Aba|Uma opção de navegação dentro da `TabbedPage`|
|`Title`|Define o título utilizado para identificar a página/aba|
|`xmlns`|Permite importar um namespace para utilizar classes no XAML|
|`x:Class`|Define a classe associada ao arquivo XAML|
|`ContentPage`|Página utilizada para criar o conteúdo de uma aba|
|`TabbedPageMenu`|Página responsável por organizar as abas|
|`MainPage`|Define a página inicial da aplicação|

---

# 25. O que foi aprendido nesta aula

Nesta aula aprendemos o último dos principais modelos de páginas apresentados no curso: a `TabbedPage`.

Diferentemente da `FlyoutPage`, que utiliza um menu lateral, a `TabbedPage` utiliza abas para permitir a navegação entre diferentes páginas.

A estrutura básica é:

```xml
<TabbedPage>

    <pages:Page1 />

    <pages:Page2 />

    <pages:Page3 />

</TabbedPage>
```

Cada página representa uma aba.

Além disso, a própria `TabbedPage` gerencia a troca entre as páginas.

Por isso, não precisamos criar manualmente eventos como:

```csharp
Clicked
```

para realizar a navegação básica.

Outro ponto importante é a utilização da propriedade:

```xml
Title="Página 1"
```

O `Title` de cada página pode ser utilizado para identificar a respectiva aba.

Assim, temos:

```text
TabbedPage
│
├── Page1 → Aba "Página 1"
├── Page2 → Aba "Página 2"
└── Page3 → Aba "Página 3"
```

A principal ideia que devemos guardar é:

> **A `TabbedPage` é uma estrutura de navegação baseada em abas, na qual cada aba pode representar uma página diferente e a própria `TabbedPage` controla a navegação entre elas.**


# 26. Resumo

### Resumo da aula — `TabbedPage` no .NET MAUI

| Conceito                        | O que é                                                                    | Exemplo                                            |
| ------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------- |
| **TabbedPage**                  | Página utilizada para criar uma interface baseada em abas.                 | `<TabbedPage>...</TabbedPage>`                     |
| **Aba (Tab)**                   | Cada opção de navegação dentro da `TabbedPage`.                            | Página 1, Página 2, Página 3                       |
| **Página filha**                | Página que será apresentada dentro de uma aba.                             | `<pages:Page1 />`                                  |
| **ContentPage**                 | Página utilizada para representar o conteúdo de cada aba.                  | `public partial class Page1 : ContentPage`         |
| **TabbedPageMenu**              | Página responsável por organizar e configurar as abas.                     | `public partial class TabbedPageMenu : TabbedPage` |
| **`FlyoutPage`**                | Modelo de página que utiliza um menu lateral.                              | `FlyoutPage`                                       |
| **`TabbedPage` x `FlyoutPage`** | `FlyoutPage` utiliza menu lateral; `TabbedPage` utiliza abas.              | Menu lateral × Abas                                |
| **`Flyout`**                    | Área do menu lateral do `FlyoutPage`.                                      | `FlyoutPage.Flyout`                                |
| **`Detail`**                    | Área de conteúdo principal do `FlyoutPage`.                                | `FlyoutPage.Detail`                                |
| **Navegação no FlyoutPage**     | Pode exigir programação para alterar o `Detail`.                           | `flyoutPage.Detail = new Page2();`                 |
| **Navegação no TabbedPage**     | É gerenciada automaticamente pela própria `TabbedPage`.                    | Clique na aba → página correspondente              |
| **`Title`**                     | Define o título de uma página e pode ser utilizado para identificar a aba. | `Title="Página 1"`                                 |
| **`xmlns`**                     | Permite importar namespaces para utilizar páginas/classes no XAML.         | `xmlns:pages="clr-namespace:AppTabbedPage"`        |
| **`x:Class`**                   | Define a classe associada ao arquivo XAML.                                 | `x:Class="AppTabbedPage.TabbedPageMenu"`           |
| **`MainPage`**                  | Define a página inicial da aplicação.                                      | `MainPage = new TabbedPageMenu();`                 |
| **Herança**                     | A classe da estrutura de abas deve herdar de `TabbedPage`.                 | `class TabbedPageMenu : TabbedPage`                |
| **Páginas como abas**           | As páginas são declaradas dentro da `TabbedPage`.                          | `<pages:Page1 />`                                  |
| **Quantidade de abas**          | A quantidade de páginas declaradas determina as abas disponíveis.          | 3 páginas → 3 abas                                 |
| **Eventos `Clicked`**           | Não são necessários para a troca básica entre abas.                        | A própria `TabbedPage` controla a navegação        |
| **Layout da aba**               | Cada página pode ter seus próprios layouts e componentes.                  | `VerticalStackLayout`, `Label`, `Button` etc.      |

### Estrutura geral

|Nível|Elemento|Função|
|---|---|---|
|1|`App`|Inicializa a aplicação|
|2|`TabbedPageMenu`|Estrutura principal das abas|
|3|`TabbedPage`|Gerencia as abas|
|4|`Page1`, `Page2`, `Page3`|Conteúdo de cada aba|
|5|`ContentPage`|Estrutura individual de cada página|
|6|Layouts e controles|Interface da página|

### Exemplo da estrutura completa

```
App
 │
 └── TabbedPageMenu
      │
      └── TabbedPage
           │
           ├── Page1 → Aba "Página 1"
           │    └── ContentPage
           │
           ├── Page2 → Aba "Página 2"
           │    └── ContentPage
           │
           └── Page3 → Aba "Página 3"
                └── ContentPage
```

### Comparação dos modelos de página estudados

| Tipo               | Principal finalidade       | Navegação                    | Estrutura           |
| ------------------ | -------------------------- | ---------------------------- | ------------------- |
| **ContentPage**    | Criar uma tela de conteúdo | Não possui navegação própria | Uma página          |
| **NavigationPage** | Navegação entre páginas    | Pilha de navegação           | Página → Página     |
| **FlyoutPage**     | Criar menu lateral         | Menu lateral                 | `Flyout` + `Detail` |
| **TabbedPage**     | Criar navegação por abas   | Abas                         | Várias páginas      |

### Exemplo prático

```xml
<TabbedPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:pages="clr-namespace:AppTabbedPage"
    x:Class="AppTabbedPage.TabbedPageMenu">

    <pages:Page1 />

    <pages:Page2 />

    <pages:Page3 />

</TabbedPage>
```

E cada página pode definir seu próprio título:

```
<ContentPage
    ...
    Title="Página 1">
```

```
<ContentPage
    ...
    Title="Página 2">
```

```
<ContentPage
    ...
    Title="Página 3">
```

**Ideia principal para memorizar:**

> `TabbedPage` = **estrutura de abas + várias páginas + navegação automática entre elas**.

Enquanto no `FlyoutPage` normalmente pensamos em:

> `FlyoutPage` = **menu lateral + `Flyout` + `Detail`**.