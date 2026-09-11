# Índices da nota

[[#Índices da nota]]

- [[#1. Conceito de Navegação]]
    
- [[#2. Shell]]
    
- [[#3. Estrutura do Shell]]
    
- [[#4. Rotas]]
    
- [[#5. Navegação com GoToAsync()]]
    
- [[#6. Navegação para trás]]
    
- [[#7. Passagem de parâmetros]]
    
- [[#8. Query Parameters]]
    
- [[#9. QueryProperty]]
    
- [[#10. IQueryAttributable]]
    
- [[#11. NavigationPage]]
    
- [[#12. PushAsync() e PopAsync()]]
    
- [[#13. FlyoutPage]]
    
- [[#14. TabbedPage]]
    
- [[#15. Deep Links]]
    
- [[#16. Shell vs NavigationPage]]
    
- [[#17. Navegação e MVVM]]
    
- [[#Tabela resumo]]
    

---

# 1. Conceito de Navegação

A **navegação** no .NET MAUI é o mecanismo utilizado para levar o usuário de uma página para outra dentro da aplicação.

Por exemplo:

```text
LoginPage
    ↓
HomePage
    ↓
ProdutoPage
    ↓
DetalhesPage
```

Cada tela normalmente é representada por uma `Page`, como:

```text
ContentPage
```

A navegação controla:

- abertura de novas páginas;
    
- retorno para páginas anteriores;
    
- passagem de dados entre páginas;
    
- organização das páginas;
    
- acesso direto a determinadas telas.
    

No .NET MAUI, existem diferentes mecanismos de navegação, sendo o **Shell** a abordagem mais moderna e integrada.

---

# 2. Shell

O `Shell` é uma estrutura do .NET MAUI que fornece uma forma centralizada de organizar a navegação da aplicação.

Um projeto MAUI normalmente possui um:

```text
AppShell.xaml
AppShell.xaml.cs
```

O `AppShell` funciona como o ponto central onde a estrutura de navegação da aplicação pode ser definida.

Exemplo:

```xml
<Shell
    x:Class="MeuApp.AppShell"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml">

    <ShellContent
        Title="Início"
        ContentTemplate="{DataTemplate local:MainPage}"
        Route="main" />

</Shell>
```

A estrutura pode ser representada como:

```text
App
 ↓
AppShell
 ↓
Shell
 ↓
Páginas
```

O Shell também permite trabalhar com:

- rotas;
    
- navegação hierárquica;
    
- Flyout;
    
- abas;
    
- parâmetros;
    
- deep links.
    

---

# 3. Estrutura do Shell

O Shell possui uma estrutura hierárquica.

```text
Shell
│
├── ShellItem
│   │
│   ├── ShellSection
│   │   │
│   │   ├── ShellContent
│   │   └── ShellContent
│   │
│   └── ShellSection
│
└── ShellItem
```

## Shell

É o contêiner principal da navegação.

```xml
<Shell>
    ...
</Shell>
```

## ShellItem

Representa um item principal da estrutura de navegação.

Pode representar, por exemplo, um item do menu lateral.

## ShellSection

Representa uma seção dentro de um `ShellItem`.

## ShellContent

Representa o conteúdo/página que será exibido.

Exemplo:

```xml
<ShellContent
    Title="Início"
    ContentTemplate="{DataTemplate local:MainPage}" />
```

Uma forma simples de memorizar:

```text
Shell
 ↓
ShellItem
 ↓
ShellSection
 ↓
ShellContent
 ↓
Page
```

---

# 4. Rotas

Uma **rota** identifica um destino de navegação.

Por exemplo:

```text
home
produto
perfil
configuracoes
```

Podemos registrar uma rota utilizando:

```csharp
Routing.RegisterRoute(
    "produto",
    typeof(ProdutoPage)
);
```

Agora:

```text
"produto"
    ↓
ProdutoPage
```

Podemos navegar para essa página usando:

```csharp
await Shell.Current.GoToAsync("produto");
```

## Registro de rotas

Normalmente as rotas são registradas no `AppShell.xaml.cs`:

```csharp
public AppShell()
{
    InitializeComponent();

    Routing.RegisterRoute(
        "produto",
        typeof(ProdutoPage)
    );
}
```

---

# 5. Navegação com GoToAsync()

O método principal de navegação do Shell é:

```csharp
GoToAsync()
```

Exemplo:

```csharp
await Shell.Current.GoToAsync("produto");
```

Fluxo:

```text
HomePage
    │
    │ GoToAsync("produto")
    ↓
ProdutoPage
```

Também podemos utilizar:

```csharp
await Shell.Current.GoToAsync("configuracoes");
```

Portanto:

```text
Shell
  ↓
GoToAsync()
  ↓
Rota
  ↓
Página
```

---

# 6. Navegação para trás

Para retornar para a página anterior utilizando o Shell:

```csharp
await Shell.Current.GoToAsync("..");
```

Por exemplo:

```text
HomePage
    ↓
ProdutoPage
    ↓
DetalhesPage
```

Na `DetalhesPage`:

```csharp
await Shell.Current.GoToAsync("..");
```

Resultado:

```text
HomePage
    ↓
ProdutoPage
```

O:

```text
..
```

representa o retorno para o nível anterior da navegação.

---

## Voltar para a raiz

Também podemos voltar para a página raiz da navegação:

```csharp
await Shell.Current.Navigation.PopToRootAsync();
```

Exemplo:

```text
Home
 ↓
Produtos
 ↓
Produto
 ↓
Detalhes
```

Depois:

```csharp
PopToRootAsync()
```

Resultado:

```text
Home
```

---

# 7. Passagem de parâmetros

É possível enviar informações de uma página para outra durante a navegação.

Por exemplo, temos:

```text
Produtos
    ↓
Detalhes
```

Queremos enviar:

```text
id = 25
```

Podemos fazer:

```csharp
await Shell.Current.GoToAsync(
    "detalhes?id=25"
);
```

O parâmetro é:

```text
id = 25
```

Fluxo:

```text
Produtos
   │
   │ id = 25
   ↓
Detalhes
```

Isso é muito utilizado para informar qual registro deve ser carregado.

---

# 8. Query Parameters

Os **Query Parameters** são parâmetros enviados através da rota.

Exemplo:

```csharp
await Shell.Current.GoToAsync(
    "produto?id=25"
);
```

A estrutura é:

```text
produto?id=25
   │      │
   │      └── valor
   └───────── parâmetro
```

Podemos enviar vários parâmetros:

```csharp
await Shell.Current.GoToAsync(
    "produto?id=25&nome=Notebook"
);
```

Nesse caso:

```text
id   = 25
nome = Notebook
```

---

# 9. QueryProperty

`QueryProperty` pode ser utilizado para receber parâmetros enviados através da navegação.

Exemplo:

```csharp
[QueryProperty(nameof(Id), "id")]
public partial class ProdutoPage : ContentPage
{
    public string Id { get; set; }

    public ProdutoPage()
    {
        InitializeComponent();
    }
}
```

Ao navegar:

```csharp
await Shell.Current.GoToAsync(
    "produto?id=25"
);
```

o parâmetro:

```text
id=25
```

será associado à propriedade:

```csharp
Id
```

Resultado:

```text
Id = "25"
```

A associação funciona assim:

```text
Query Parameter
       ↓
     "id"
       ↓
 QueryProperty
       ↓
      Id
```

---

# 10. IQueryAttributable

Outra forma de receber parâmetros é implementar:

```csharp
IQueryAttributable
```

Exemplo:

```csharp
public partial class ProdutoPage
    : ContentPage, IQueryAttributable
{
    public ProdutoPage()
    {
        InitializeComponent();
    }

    public void ApplyQueryAttributes(
        IDictionary<string, object> query)
    {
        var id = query["id"];
    }
}
```

O método:

```csharp
ApplyQueryAttributes()
```

é utilizado para processar os parâmetros recebidos durante a navegação.

Essa abordagem oferece maior controle sobre o tratamento dos dados recebidos.

---

# 11. NavigationPage

`NavigationPage` é o mecanismo tradicional de navegação baseado em uma **pilha de páginas**.

Imagine:

```text
HomePage
```

Ao navegar para outra página:

```text
HomePage
    ↓
ProdutoPage
```

A `ProdutoPage` é colocada no topo da pilha.

Podemos visualizar:

```text
┌─────────────────┐
│ ProdutoPage     │ ← atual
├─────────────────┤
│ HomePage        │
└─────────────────┘
```

A navegação tradicional utiliza principalmente:

```csharp
PushAsync()
PopAsync()
PopToRootAsync()
```

---

# 12. PushAsync() e PopAsync()

## PushAsync()

Adiciona uma página à pilha:

```csharp
await Navigation.PushAsync(
    new ProdutoPage()
);
```

Resultado:

```text
HomePage
    ↓
ProdutoPage
```

## PopAsync()

Remove a página atual:

```csharp
await Navigation.PopAsync();
```

Resultado:

```text
ProdutoPage
    ↓
HomePage
```

## PopToRootAsync()

Retorna para a primeira página da pilha:

```csharp
await Navigation.PopToRootAsync();
```

Exemplo:

```text
Home
 ↓
Produtos
 ↓
Detalhes
 ↓
Editar
```

Depois:

```text
PopToRootAsync()
```

Resultado:

```text
Home
```

---

# 13. FlyoutPage

`FlyoutPage` representa uma estrutura de interface com **menu lateral**.

Visualmente:

```text
┌──────────────┬─────────────────┐
│              │                 │
│    MENU      │    CONTEÚDO     │
│              │                 │
│    Início    │                 │
│    Perfil    │                 │
│    Config.   │                 │
│              │                 │
└──────────────┴─────────────────┘
```

Possui dois elementos principais:

```text
Flyout
  ↓
Menu lateral

Detail
  ↓
Conteúdo principal
```

Conceitualmente:

```csharp
Flyout = new MenuPage();

Detail = new NavigationPage(
    new MainPage()
);
```

O `FlyoutPage` é tradicionalmente utilizado para criar interfaces com menu lateral.

Em aplicações modernas, o `Shell` também oferece suporte a esse tipo de navegação.

---

# 14. TabbedPage

`TabbedPage` organiza páginas utilizando **abas**.

Visualmente:

```text
┌─────────────────────────────┐
│                             │
│          CONTEÚDO           │
│                             │
├─────────────────────────────┤
│ Início │ Perfil │ Config.  │
└─────────────────────────────┘
```

Exemplo:

```xml
<TabbedPage>

    <ContentPage
        Title="Início" />

    <ContentPage
        Title="Perfil" />

    <ContentPage
        Title="Configurações" />

</TabbedPage>
```

Cada aba representa uma página/seção.

O Shell também possui mecanismos próprios para trabalhar com abas, como `TabBar`.

---

# 15. Deep Links

Um **Deep Link** permite abrir diretamente uma determinada parte de um aplicativo.

Sem deep link:

```text
Abrir aplicativo
      ↓
Home
      ↓
Produtos
      ↓
Produto
      ↓
Detalhes
```

Com deep link:

```text
Link
 ↓
Aplicativo
 ↓
Detalhes do produto
```

Conceitualmente:

```text
meuapp://produto/25
```

A ideia principal é:

> Um deep link permite direcionar o usuário diretamente para um destino específico dentro do aplicativo.

Podemos representar:

```text
Deep Link
    ↓
URI
    ↓
Rota
    ↓
Página
```

Deep links são úteis, por exemplo, em:

- links enviados por mensagens;
    
- notificações;
    
- campanhas;
    
- e-mails;
    
- links externos;
    
- compartilhamento de conteúdo.
    

---

# 16. Shell vs NavigationPage

Os dois mecanismos possuem conceitos diferentes.

|Shell|NavigationPage|
|---|---|
|Abordagem moderna|Abordagem tradicional|
|Baseado em rotas|Baseado em pilha|
|`GoToAsync()`|`PushAsync()`|
|`GoToAsync("..")`|`PopAsync()`|
|Suporte integrado a Flyout|Não é seu objetivo principal|
|Suporte integrado a Tabs|Não é seu objetivo principal|
|Facilita deep linking|Deep linking é mais manual|

Uma forma simples de memorizar:

```text
Shell
 ↓
ROTAS
 ↓
GoToAsync()
```

Enquanto:

```text
NavigationPage
 ↓
PILHA
 ↓
PushAsync()
PopAsync()
```

---

# 17. Navegação e MVVM

Em aplicações maiores, é comum separar a lógica de navegação da interface.

Uma arquitetura baseada em MVVM pode seguir:

```text
View
 ↓
ViewModel
 ↓
Navegação
 ↓
Outra View
```

Por exemplo:

```text
ProdutoPage
      ↓
ProdutoViewModel
      ↓
Navegação
      ↓
DetalhesPage
```

Isso ajuda a manter a aplicação organizada e reduz a quantidade de lógica diretamente no Code Behind.

A navegação pode fazer parte da responsabilidade do ViewModel ou ser abstraída por um serviço de navegação.

---

# Tabela resumo

## Conceitos principais

|Conceito|Definição|Exemplo|
|---|---|---|
|`Shell`|Estrutura moderna de navegação|`AppShell`|
|`ShellItem`|Item principal do Shell|Item do menu|
|`ShellSection`|Seção dentro do Shell|Seção de navegação|
|`ShellContent`|Conteúdo/página|`MainPage`|
|Rota|Identifica um destino|`"produto"`|
|`Routing.RegisterRoute()`|Registra uma rota|`RegisterRoute("produto", ...)`|
|`GoToAsync()`|Realiza navegação pelo Shell|`GoToAsync("produto")`|
|`..`|Retorna na navegação|`GoToAsync("..")`|
|`//`|Indica navegação absoluta|`GoToAsync("//home")`|
|Query Parameter|Passa dados pela rota|`?id=25`|
|`QueryProperty`|Recebe parâmetros de navegação|`[QueryProperty]`|
|`IQueryAttributable`|Permite processar parâmetros|`ApplyQueryAttributes()`|
|`NavigationPage`|Navegação tradicional baseada em pilha|`NavigationPage`|
|`PushAsync()`|Adiciona página à pilha|`PushAsync(page)`|
|`PopAsync()`|Remove página da pilha|`PopAsync()`|
|`PopToRootAsync()`|Retorna para a raiz|`PopToRootAsync()`|
|`FlyoutPage`|Interface com menu lateral|`Flyout + Detail`|
|`TabbedPage`|Interface baseada em abas|`Tab 1 + Tab 2`|
|Deep Link|Abre diretamente um destino do app|URI|

---

## Métodos de navegação

|Método|Mecanismo|Função|
|---|---|---|
|`GoToAsync("pagina")`|Shell|Navegar para uma rota|
|`GoToAsync("..")`|Shell|Voltar|
|`GoToAsync("//pagina")`|Shell|Navegação absoluta|
|`PushAsync(page)`|NavigationPage|Adicionar página|
|`PopAsync()`|NavigationPage|Voltar uma página|
|`PopToRootAsync()`|NavigationPage|Voltar para a raiz|

---

## Estruturas de navegação

|Estrutura|Principal característica|
|---|---|
|`Shell`|Navegação integrada baseada em rotas|
|`NavigationPage`|Navegação baseada em pilha|
|`FlyoutPage`|Menu lateral|
|`TabbedPage`|Abas|

---

## Formas de passagem de dados

|Mecanismo|Utilização|
|---|---|
|Query Parameter|Passar valores simples pela rota|
|`QueryProperty`|Associar parâmetros a propriedades|
|`IQueryAttributable`|Processar parâmetros manualmente|
|`Dictionary<string, object>`|Passar objetos/valores complexos|

---

# Resumo para memorizar

```text
NAVEGAÇÃO — .NET MAUI
│
├── Shell
│   ├── Rotas
│   ├── GoToAsync()
│   ├── ".." → voltar
│   ├── "//" → navegação absoluta
│   ├── Query Parameters
│   ├── QueryProperty
│   └── IQueryAttributable
│
├── NavigationPage
│   ├── PushAsync()
│   ├── PopAsync()
│   └── PopToRootAsync()
│
├── FlyoutPage
│   └── Menu lateral
│
├── TabbedPage
│   └── Abas
│
└── Deep Links
    └── Acesso direto a um destino
```

### Regra de ouro

```text
Shell
→ ROTAS
→ GoToAsync()

NavigationPage
→ PILHA
→ PushAsync()
→ PopAsync()

FlyoutPage
→ MENU LATERAL

TabbedPage
→ ABAS

Deep Link
→ ACESSO DIRETO AO DESTINO
```

---

# Pontos mais importantes para concursos

1. **Shell** → sistema moderno de navegação do MAUI.
    
2. **Rota** → identifica um destino.
    
3. **`Routing.RegisterRoute()`** → registra rotas.
    
4. **`GoToAsync()`** → navegação com Shell.
    
5. **`GoToAsync("..")`** → retorna.
    
6. **`GoToAsync("//rota")`** → navegação absoluta.
    
7. **Query Parameters** → permitem transportar dados.
    
8. **`QueryProperty`** → recebe parâmetros em propriedades.
    
9. **`IQueryAttributable`** → permite tratar parâmetros recebidos.
    
10. **`NavigationPage`** → trabalha com pilha.
    
11. **`PushAsync()`** → adiciona página à pilha.
    
12. **`PopAsync()`** → remove página da pilha.
    
13. **`FlyoutPage`** → menu lateral.
    
14. **`TabbedPage`** → abas.
    
15. **Deep Link** → acesso direto a uma tela/conteúdo específico.