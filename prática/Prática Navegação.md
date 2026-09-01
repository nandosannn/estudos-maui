
# 📱 Mini projeto — Catálogo de Produtos

### Objetivo

Criar um aplicativo MAUI chamado **Catálogo**, onde o usuário poderá:

```
┌──────────────────────────────┐
│       CATÁLOGO               │
│                              │
│  [ Ver produtos ]            │
│                              │
│  [ Perfil ]                  │
│                              │
└──────────────────────────────┘
```

Ao clicar em **Ver produtos**:

```
Produtos
────────────────────
📱 Notebook
    Ver detalhes →

🎧 Headset
    Ver detalhes →

⌨️ Teclado
    Ver detalhes →
```

Ao clicar em um produto:

```
Detalhes do produto

Notebook

ID: 1

Preço: R$ 3.500

[ Voltar ]
```

A ideia é você implementar isso **sem eu entregar o projeto pronto**.

---

## 🎯 Conceitos que você vai praticar

|Conceito|Onde será usado|
|---|---|
|`Shell`|Estrutura principal|
|`ShellContent`|Página inicial|
|Rotas|`produtos` e `detalhes`|
|`Routing.RegisterRoute()`|Registrar páginas|
|`GoToAsync()`|Ir para outra página|
|`GoToAsync("..")`|Voltar|
|Query Parameters|Enviar `id` e `nome`|
|`QueryProperty`|Receber dados|
|`IQueryAttributable`|**Desafio extra**|
|`//`|Navegação absoluta|
|`NavigationPage`|**Desafio extra**|
|`FlyoutPage` / menu|**Desafio extra**|
|`TabbedPage`|**Desafio extra**|
|Deep Link|**Desafio conceitual**|

A passagem de parâmetros por query string e o uso de `QueryProperty` fazem parte diretamente do conteúdo da aula.

---

## 🧱 Etapa 1 — Criar o projeto

Crie um projeto:

```
CatalogoApp
```

Você deverá ter aproximadamente:

```
CatalogoApp
│
├── App.xaml
├── App.xaml.cs
│
├── AppShell.xaml
├── AppShell.xaml.cs
│
├── MainPage.xaml
├── MainPage.xaml.cs
│
├── ProdutosPage.xaml
├── ProdutosPage.xaml.cs
│
├── DetalhesPage.xaml
└── DetalhesPage.xaml.cs
```

---

## 🏠 Etapa 2 — Página inicial

Sua `MainPage` deve possuir:

- título **Catálogo**
- um botão **Ver produtos**
- um botão **Perfil**

O botão **Ver produtos** deverá navegar para:

```
ProdutosPage
```

Mas você **não deve usar**:

```
Navigation.PushAsync(...)
```

Nesta primeira parte, utilize o mecanismo do `Shell`:

```
Shell.Current.GoToAsync(...)
```

A aula estabelece justamente essa relação:

```
Shell
   ↓
Rotas
   ↓
GoToAsync()
```

---

## 🛣️ Etapa 3 — Criar a rota

No `AppShell.xaml.cs`, registre uma rota para:

```
produtos
```

Ela deverá apontar para:

```
ProdutosPage
```

Você precisa descobrir como fazer isso usando:

```
Routing.RegisterRoute(...)
```

A estrutura esperada é:

```
"produtos"
      ↓
ProdutosPage
```

Isso é exatamente o mecanismo de registro de rotas apresentado na aula.

---

## 📦 Etapa 4 — Lista de produtos

Na `ProdutosPage`, crie três produtos:

```
Notebook
Headset
Teclado
```

Cada produto deve ter:

```
Nome
ID
Preço
```

Por enquanto, pode deixar os dados diretamente no código.

Por exemplo, conceitualmente:

```
Notebook
ID: 1
Preço: 3500

Headset
ID: 2
Preço: 250

Teclado
ID: 3
Preço: 180
```

Você pode usar `Button`, `Label`, `VerticalStackLayout`, `Grid` etc.

---

## 🔀 Etapa 5 — Navegar para detalhes

Essa é a parte mais importante do exercício.

Quando o usuário clicar em:

```
Notebook
```

você deverá navegar para:

```
DetalhesPage
```

**enviando o ID e o nome do produto.**

A URL conceitual será:

```
detalhes?id=1&nome=Notebook
```

Para outro produto:

```
detalhes?id=2&nome=Headset
```

A aula apresenta exatamente esse conceito de Query Parameters:

```
produto?id=25&nome=Notebook
```

---

## 📄 Etapa 6 — Receber os parâmetros

Agora faça a `DetalhesPage` receber:

```
id
nome
```

Você deverá utilizar:

```
[QueryProperty(...)]
```

A página deverá mostrar:

```
Detalhes do produto

Nome: Notebook
ID: 1

Preço: R$ 3500

[Voltar]
```

O desafio aqui é fazer o parâmetro:

```
id=1
```

chegar até:

```
Id
```

e:

```
nome=Notebook
```

chegar até:

```
Nome
```

Esse é justamente o funcionamento de `QueryProperty` apresentado na aula.

---

## ↩️ Etapa 7 — Voltar

Na `DetalhesPage`, crie:

```
[ ← Voltar ]
```

Ao clicar, utilize:

```
GoToAsync("..")
```

O resultado deve ser:

```
Produtos
   ↓
Detalhes
   ↓
Voltar
   ↓
Produtos
```

Na aula, `..` representa o retorno ao nível anterior da navegação.

---

## ⭐ Etapa 8 — Desafio com `IQueryAttributable`

Agora **não olhe a implementação anterior**.

Modifique a `DetalhesPage` para que ela **não utilize `QueryProperty`**.

Em vez disso, implemente:

```
IQueryAttributable
```

e:

```
ApplyQueryAttributes(...)
```

Seu objetivo continua sendo receber:

```
id
nome
```

e exibir:

```
Notebook
ID: 1
```

A aula apresenta `IQueryAttributable` justamente como uma alternativa que oferece maior controle sobre o processamento dos parâmetros.

---

## 🚀 Etapa 9 — Desafio `//`

Agora faça o seguinte:

Na `DetalhesPage`, coloque:

```
[ Voltar para o início ]
```

Esse botão **não deve voltar apenas uma página**.

Ele deve retornar diretamente para:

```
MainPage
```

Você deverá pesquisar/praticar a navegação absoluta utilizando:

```
//
```

A aula apresenta:

```
GoToAsync("//pagina")
```

como navegação absoluta.

---

## 🧪 Etapa 10 — Teste mental da navegação

Antes de executar, tente desenhar o fluxo:

```
             ┌──────────────┐
             │   MainPage   │
             └──────┬───────┘
                    │
              produtos
                    ↓
             ┌──────────────┐
             │ ProdutosPage │
             └──────┬───────┘
                    │
              id + nome
                    ↓
             ┌──────────────┐
             │ DetalhesPage │
             └──────┬───────┘
                    │
                    │ ..
                    ↓
             ProdutosPage
```

Se você conseguir explicar esse fluxo, já está entendendo uma parte importante da aula.

---

## 🔥 Desafios extras

Depois que o projeto básico estiver funcionando, faça estes desafios **sem copiar código**.

### Desafio 1 — `PopToRootAsync()`

Crie:

```
Main
 ↓
Produtos
 ↓
Detalhes
```

Na `DetalhesPage`, adicione:

```
[ Ir para o início ]
```

Faça o botão retornar diretamente para a raiz.

---

### Desafio 2 — `NavigationPage`

Crie uma segunda versão da navegação usando:

```
NavigationPage
```

Em vez de:

```
GoToAsync()
```

utilize:

```
PushAsync()
PopAsync()
```

A diferença que você deve perceber é:

```
Shell

ROTAS
  ↓
GoToAsync()


NavigationPage

PILHA
  ↓
PushAsync()
  ↓
PopAsync()
```

Essa é uma das diferenças centrais destacadas na aula.

---

### Desafio 3 — Menu lateral

Adicione um menu lateral contendo:

```
☰ Menu

Início
Produtos
Perfil
Configurações
```

Você pode fazer isso utilizando a estrutura de menu do `Shell` ou, como exercício específico da aula, experimentar `FlyoutPage`.

A ideia do `FlyoutPage` é:

```
Flyout
   ↓
Menu lateral

Detail
   ↓
Conteúdo
```

---

### Desafio 4 — Abas

Crie uma versão com:

```
┌───────────────────────────────┐
│                               │
│          CONTEÚDO             │
│                               │
├───────────────────────────────┤
│ Início │ Produtos │ Perfil   │
└───────────────────────────────┘
```

Utilize:

```
TabbedPage
```

ou o mecanismo de abas do `Shell`.

A aula apresenta `TabbedPage` como uma estrutura baseada em abas.

---

## 🧠 Seu checklist

Tente terminar o projeto conseguindo marcar:

```
[ ] Criar Shell
[ ] Criar MainPage
[ ] Criar ProdutosPage
[ ] Criar DetalhesPage

[ ] Registrar uma rota
[ ] Usar GoToAsync()
[ ] Usar GoToAsync("..")
[ ] Usar GoToAsync("//...")
[ ] Passar parâmetros pela URL
[ ] Receber parâmetros com QueryProperty
[ ] Receber parâmetros com IQueryAttributable

[ ] Entender a pilha do NavigationPage
[ ] Usar PushAsync()
[ ] Usar PopAsync()
[ ] Usar PopToRootAsync()

[ ] Criar menu lateral
[ ] Criar abas

[ ] Entender o conceito de Deep Link
```

## 🎯 Regra do exercício

**Não tente fazer tudo de uma vez.**

Faça nesta ordem:

```
1. MainPage
      ↓
2. ProdutosPage
      ↓
3. Rotas
      ↓
4. GoToAsync()
      ↓
5. DetalhesPage
      ↓
6. Query Parameters
      ↓
7. QueryProperty
      ↓
8. IQueryAttributable
      ↓
9. Navegação para trás
      ↓
10. Desafios extras
```

O projeto básico já cobre uma boa parte prática da aula; `FlyoutPage`, `TabbedPage`, `NavigationPage` e Deep Links entram como desafios para consolidar os conceitos. A própria aula resume essas quatro estruturas como **Shell = rotas**, **NavigationPage = pilha**, **FlyoutPage = menu lateral** e **TabbedPage = abas**.


# 📱 Projeto: CatálogoApp

Estrutura:

```
CatalogoApp/
│
├── App.xaml
├── App.xaml.cs
│
├── AppShell.xaml
├── AppShell.xaml.cs
│
├── MainPage.xaml
├── MainPage.xaml.cs
│
├── ProdutosPage.xaml
├── ProdutosPage.xaml.cs
│
├── DetalhesPage.xaml
└── DetalhesPage.xaml.cs
```

---

## 1. `AppShell.xaml`

Aqui fica a estrutura principal do `Shell`.

```
<?xml version="1.0" encoding="UTF-8" ?>

<Shell
    x:Class="CatalogoApp.AppShell"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:local="clr-namespace:CatalogoApp"
    FlyoutBehavior="Disabled">

    <ShellContent
        Title="Início"
        Route="home"
        ContentTemplate="{DataTemplate local:MainPage}" />

</Shell>
```

A ideia é:

```
Shell
 ↓
ShellContent
 ↓
MainPage
```

Isso segue a hierarquia apresentada na aula.

---

## 2. `AppShell.xaml.cs`

Aqui registramos as rotas das páginas que não fazem parte diretamente da estrutura visual do Shell.

```
namespace CatalogoApp;

public partial class AppShell : Shell
{
    public AppShell()
    {
        InitializeComponent();

        Routing.RegisterRoute(
            "produtos",
            typeof(ProdutosPage)
        );

        Routing.RegisterRoute(
            "detalhes",
            typeof(DetalhesPage)
        );
    }
}
```

Temos:

```
"produtos" → ProdutosPage
"detalhes" → DetalhesPage
```

Isso corresponde ao `Routing.RegisterRoute()` da aula.

---

## 3. `App.xaml`

Pode deixar o padrão:

```
<?xml version="1.0" encoding="UTF-8" ?>

<Application
    x:Class="CatalogoApp.App"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml">

    <Application.Resources>
        <ResourceDictionary />
    </Application.Resources>

</Application>
```

---

## 4. `App.xaml.cs`

```
namespace CatalogoApp;

public partial class App : Application
{
    public App()
    {
        InitializeComponent();
    }

    protected override Window CreateWindow(
        IActivationState? activationState)
    {
        return new Window(new AppShell());
    }
}
```

O fluxo fica:

```
App
 ↓
AppShell
 ↓
MainPage
```

---

## 5. `MainPage.xaml`

Essa será nossa tela inicial.

```
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    x:Class="CatalogoApp.MainPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    Title="Início">

    <VerticalStackLayout
        Padding="30"
        Spacing="20"
        VerticalOptions="Center">

        <Label
            Text="📱 Catálogo"
            FontSize="32"
            FontAttributes="Bold"
            HorizontalOptions="Center" />

        <Label
            Text="Mini projeto de navegação com .NET MAUI"
            FontSize="16"
            HorizontalTextAlignment="Center" />

        <Button
            Text="Ver produtos"
            Clicked="OnProdutosClicked" />

        <Button
            Text="Perfil"
            Clicked="OnPerfilClicked" />

    </VerticalStackLayout>

</ContentPage>
```

---

## 6. `MainPage.xaml.cs`

Aqui usamos `GoToAsync()`.

```
namespace CatalogoApp;

public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
    }

    private async void OnProdutosClicked(
        object sender,
        EventArgs e)
    {
        await Shell.Current.GoToAsync("produtos");
    }

    private async void OnPerfilClicked(
        object sender,
        EventArgs e)
    {
        await DisplayAlert(
            "Perfil",
            "Página de perfil ainda não implementada.",
            "OK"
        );
    }
}
```

O ponto importante é:

```
await Shell.Current.GoToAsync("produtos");
```

O fluxo é:

```
MainPage
   ↓
GoToAsync("produtos")
   ↓
rota
   ↓
ProdutosPage
```

Isso corresponde diretamente ao mecanismo apresentado na aula.

---

## 7. `ProdutosPage.xaml`

Agora criamos nossa lista.

```
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    x:Class="CatalogoApp.ProdutosPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    Title="Produtos">

    <ScrollView>

        <VerticalStackLayout
            Padding="20"
            Spacing="15">

            <Label
                Text="Produtos"
                FontSize="30"
                FontAttributes="Bold" />

            <!-- Notebook -->

            <Border
                StrokeThickness="1"
                Padding="15">

                <VerticalStackLayout
                    Spacing="8">

                    <Label
                        Text="💻 Notebook"
                        FontSize="22"
                        FontAttributes="Bold" />

                    <Label
                        Text="ID: 1" />

                    <Label
                        Text="Preço: R$ 3.500,00" />

                    <Button
                        Text="Ver detalhes"
                        Clicked="OnNotebookClicked" />

                </VerticalStackLayout>

            </Border>


            <!-- Headset -->

            <Border
                StrokeThickness="1"
                Padding="15">

                <VerticalStackLayout
                    Spacing="8">

                    <Label
                        Text="🎧 Headset"
                        FontSize="22"
                        FontAttributes="Bold" />

                    <Label
                        Text="ID: 2" />

                    <Label
                        Text="Preço: R$ 250,00" />

                    <Button
                        Text="Ver detalhes"
                        Clicked="OnHeadsetClicked" />

                </VerticalStackLayout>

            </Border>


            <!-- Teclado -->

            <Border
                StrokeThickness="1"
                Padding="15">

                <VerticalStackLayout
                    Spacing="8">

                    <Label
                        Text="⌨️ Teclado"
                        FontSize="22"
                        FontAttributes="Bold" />

                    <Label
                        Text="ID: 3" />

                    <Label
                        Text="Preço: R$ 180,00" />

                    <Button
                        Text="Ver detalhes"
                        Clicked="OnTecladoClicked" />

                </VerticalStackLayout>

            </Border>

        </VerticalStackLayout>

    </ScrollView>

</ContentPage>
```

---

## 8. `ProdutosPage.xaml.cs`

Agora vem uma das partes mais importantes: **passar dados pela rota**.

```
namespace CatalogoApp;

public partial class ProdutosPage : ContentPage
{
    public ProdutosPage()
    {
        InitializeComponent();
    }

    private async void OnNotebookClicked(
        object sender,
        EventArgs e)
    {
        await AbrirDetalhes(1, "Notebook");
    }

    private async void OnHeadsetClicked(
        object sender,
        EventArgs e)
    {
        await AbrirDetalhes(2, "Headset");
    }

    private async void OnTecladoClicked(
        object sender,
        EventArgs e)
    {
        await AbrirDetalhes(3, "Teclado");
    }

    private async Task AbrirDetalhes(
        int id,
        string nome)
    {
        await Shell.Current.GoToAsync(
            $"detalhes?id={id}&nome={nome}"
        );
    }
}
```

Por exemplo, ao clicar no Notebook:

```
detalhes?id=1&nome=Notebook
```

Ao clicar no Headset:

```
detalhes?id=2&nome=Headset
```

Ao clicar no Teclado:

```
detalhes?id=3&nome=Teclado
```

Essa é a utilização prática dos **Query Parameters** da aula.

---

## 9. `DetalhesPage.xaml`

Agora vamos exibir os dados recebidos.

```
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    x:Class="CatalogoApp.DetalhesPage"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    Title="Detalhes">

    <VerticalStackLayout
        Padding="30"
        Spacing="20"
        VerticalOptions="Center">

        <Label
            Text="Detalhes do produto"
            FontSize="30"
            FontAttributes="Bold"
            HorizontalOptions="Center" />

        <Border
            Padding="20"
            StrokeThickness="1">

            <VerticalStackLayout
                Spacing="10">

                <Label
                    Text="{Binding Nome}"
                    FontSize="25"
                    FontAttributes="Bold"
                    HorizontalOptions="Center" />

                <Label
                    Text="{Binding Id, StringFormat='ID: {0}'}"
                    FontSize="18"
                    HorizontalOptions="Center" />

            </VerticalStackLayout>

        </Border>

        <Button
            Text="← Voltar"
            Clicked="OnVoltarClicked" />

        <Button
            Text="Ir para o início"
            Clicked="OnInicioClicked" />

    </VerticalStackLayout>

</ContentPage>
```

---

## 10. `DetalhesPage.xaml.cs`

Aqui vamos utilizar `QueryProperty`.

```
namespace CatalogoApp;

[QueryProperty(nameof(Id), "id")]
[QueryProperty(nameof(Nome), "nome")]
public partial class DetalhesPage : ContentPage
{
    private string _id = string.Empty;
    private string _nome = string.Empty;

    public string Id
    {
        get => _id;
        set
        {
            _id = value;
            OnPropertyChanged();
        }
    }

    public string Nome
    {
        get => _nome;
        set
        {
            _nome = Uri.UnescapeDataString(value);
            OnPropertyChanged();
        }
    }

    public DetalhesPage()
    {
        InitializeComponent();

        BindingContext = this;
    }

    private async void OnVoltarClicked(
        object sender,
        EventArgs e)
    {
        await Shell.Current.GoToAsync("..");
    }

    private async void OnInicioClicked(
        object sender,
        EventArgs e)
    {
        await Shell.Current.GoToAsync("//home");
    }
}
```

Aqui estão três conceitos importantes acontecendo.

### Recebendo `id`

```
[QueryProperty(nameof(Id), "id")]
```

Significa:

```
parâmetro "id"
       ↓
propriedade Id
```

### Recebendo `nome`

```
[QueryProperty(nameof(Nome), "nome")]
```

Significa:

```
parâmetro "nome"
       ↓
propriedade Nome
```

Esse é exatamente o relacionamento mostrado na aula.

---

## ↩️ Voltar

Aqui:

```
await Shell.Current.GoToAsync("..");
```

temos:

```
MainPage
   ↓
ProdutosPage
   ↓
DetalhesPage
   ↓
     ..
   ↓
ProdutosPage
```

O `..` representa o nível anterior da navegação.

---

## 🏠 Voltar para a raiz

Já aqui:

```
await Shell.Current.GoToAsync("//home");
```

estamos usando uma **navegação absoluta**.

```
DetalhesPage
      ↓
   //home
      ↓
 MainPage
```

A aula apresenta `//` justamente como mecanismo de navegação absoluta.

---

## 🧪 Como o projeto funciona

Quando você executa:

```
                 App
                  │
                  ↓
               AppShell
                  │
                  ↓
              MainPage
                  │
          "Ver produtos"
                  │
                  ↓
        GoToAsync("produtos")
                  │
                  ↓
           ProdutosPage
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
    Notebook   Headset   Teclado
        │         │         │
        ↓         ↓         ↓
   id=1       id=2       id=3
   nome=...   nome=...   nome=...
        │         │         │
        └─────────┼─────────┘
                  ↓
           DetalhesPage
```

Por exemplo:

```
Clique em Notebook
        ↓
GoToAsync(
    "detalhes?id=1&nome=Notebook"
)
        ↓
      Shell
        ↓
   DetalhesPage
        ↓
QueryProperty
        ↓
Id = "1"
Nome = "Notebook"
```

---

## 🧠 E onde está cada conceito da aula?

|Conceito|Implementação|
|---|---|
|`Shell`|`AppShell.xaml`|
|`ShellContent`|`AppShell.xaml`|
|Rota|`"produtos"`, `"detalhes"`|
|`Routing.RegisterRoute()`|`AppShell.xaml.cs`|
|`GoToAsync()`|`MainPage` / `ProdutosPage`|
|`..`|`DetalhesPage`|
|`//`|`DetalhesPage`|
|Query Parameter|`?id=1&nome=Notebook`|
|`QueryProperty`|`DetalhesPage`|
|`BindingContext`|`DetalhesPage`|

A parte de `NavigationPage`, `PushAsync()`/`PopAsync()`, `FlyoutPage`, `TabbedPage` e Deep Links não é necessária para o **projeto básico**; elas foram tratadas na aula como mecanismos/estruturas adicionais.

---

## ⭐ Versão alternativa: `IQueryAttributable`

Depois de fazer o projeto funcionar, você pode **substituir o `QueryProperty` da `DetalhesPage`** por `IQueryAttributable`.

A versão ficaria:

```
namespace CatalogoApp;

public partial class DetalhesPage :
    ContentPage,
    IQueryAttributable
{
    public string Id { get; set; } = string.Empty;

    public string Nome { get; set; } = string.Empty;

    public DetalhesPage()
    {
        InitializeComponent();

        BindingContext = this;
    }

    public void ApplyQueryAttributes(
        IDictionary<string, object> query)
    {
        if (query.TryGetValue("id", out var id))
        {
            Id = id.ToString() ?? string.Empty;
        }

        if (query.TryGetValue("nome", out var nome))
        {
            Nome = Uri.UnescapeDataString(
                nome.ToString() ?? string.Empty
            );
        }

        OnPropertyChanged(nameof(Id));
        OnPropertyChanged(nameof(Nome));
    }

    private async void OnVoltarClicked(
        object sender,
        EventArgs e)
    {
        await Shell.Current.GoToAsync("..");
    }

    private async void OnInicioClicked(
        object sender,
        EventArgs e)
    {
        await Shell.Current.GoToAsync("//home");
    }
}
```

A diferença fundamental é:

```
QueryProperty

Query Parameter
      ↓
[QueryProperty]
      ↓
Propriedade
```

versus:

```
IQueryAttributable

Query Parameter
      ↓
ApplyQueryAttributes()
      ↓
Você decide como processar
```

Essa segunda abordagem é apresentada na aula como uma forma de ter maior controle sobre o tratamento dos parâmetros.

**Minha sugestão para estudar:** primeiro implemente exatamente a versão com `QueryProperty`, compare com seu código e tente entender **por que cada arquivo existe**. Depois troque somente a `DetalhesPage` para `IQueryAttributable`. Isso transforma o projeto em um exercício de comparação bem mais útil do que simplesmente copiar tudo.