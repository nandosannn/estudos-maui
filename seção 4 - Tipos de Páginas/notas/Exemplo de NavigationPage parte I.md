# Exemplo completo — NavigationPage no .NET MAUI

## 1. App.xaml.cs

O `App.xaml.cs` é responsável por iniciar a aplicação utilizando uma `NavigationPage`.

```csharp
namespace AppNavigationPage;

public partial class App : Application
{
    public App()
    {
        InitializeComponent();

        MainPage = new NavigationPage(new Page1());
    }
}
```

### Conceitos utilizados

- `MainPage`: define a página principal da aplicação.
    
- `NavigationPage`: cria o mecanismo de navegação.
    
- `new Page1()`: define a primeira página que será apresentada.
    

A estrutura inicial fica:

```text
NavigationPage
└── Page1
```

---

# 2. Page1.xaml

A primeira página possui um título, um texto e um botão para avançar para a segunda página.

```xml
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppNavigationPage.Page1"
    Title="Página 1">

    <VerticalStackLayout
        Padding="20">

        <Label
            Text="Bem-vindo à Página 1"
            FontSize="30"
            HorizontalOptions="Center" />

        <Button
            Text="Prosseguir"
            HorizontalOptions="End"
            Clicked="Button_Clicked" />

    </VerticalStackLayout>

</ContentPage>
```

### Propriedades utilizadas

`Title="Página 1"`

Define o título da página. Como a página está dentro de uma `NavigationPage`, esse título pode aparecer na barra de navegação.

`Padding="20"`

Define um espaço interno de 20 unidades no `VerticalStackLayout`.

`Text="Bem-vindo à Página 1"`

Define o texto apresentado pelo `Label`.

`FontSize="30"`

Define o tamanho da fonte do `Label`.

`HorizontalOptions="Center"`

Centraliza o `Label` horizontalmente.

`Text="Prosseguir"`

Define o texto apresentado pelo botão.

`HorizontalOptions="End"`

Posiciona o botão no final do espaço horizontal disponível.

`Clicked="Button_Clicked"`

Define o método que será executado quando o botão for clicado.

---

# 3. Page1.xaml.cs

No arquivo `Page1.xaml.cs`, implementamos a ação do botão.

```csharp
namespace AppNavigationPage;

public partial class Page1 : ContentPage
{
    public Page1()
    {
        InitializeComponent();
    }

    private async void Button_Clicked(object sender, EventArgs e)
    {
        await Navigation.PushAsync(new Page2());
    }
}
```

O comando principal é:

```csharp
await Navigation.PushAsync(new Page2());
```

O `PushAsync()` adiciona a `Page2` à pilha de navegação.

Antes:

```text
Page1
```

Depois:

```text
Page1
Page2
```

A `Page2` passa a ser a página atual.

---

# 4. Page2.xaml

A segunda página segue uma estrutura semelhante.

```xml
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppNavigationPage.Page2"
    Title="Página 2">

    <VerticalStackLayout
        Padding="20">

        <Label
            Text="Bem-vindo à Página 2"
            FontSize="30"
            HorizontalOptions="Center" />

        <Button
            Text="Prosseguir"
            HorizontalOptions="End"
            Clicked="Button_Clicked" />

    </VerticalStackLayout>

</ContentPage>
```

A principal diferença em relação à primeira página é:

```xml
Title="Página 2"
```

e:

```xml
Text="Bem-vindo à Página 2"
```

---

# 5. Page2.xaml.cs

O botão da segunda página leva para a terceira página.

```csharp
namespace AppNavigationPage;

public partial class Page2 : ContentPage
{
    public Page2()
    {
        InitializeComponent();
    }

    private async void Button_Clicked(object sender, EventArgs e)
    {
        await Navigation.PushAsync(new Page3());
    }
}
```

O comando:

```csharp
await Navigation.PushAsync(new Page3());
```

adiciona a `Page3` à pilha.

A pilha passa a ser:

```text
Page1
Page2
Page3
```

A `Page3` é a página atual.

---

# 6. Page3.xaml

A terceira página possui um botão para voltar.

```xml
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppNavigationPage.Page3"
    Title="Página 3">

    <VerticalStackLayout
        Padding="20">

        <Label
            Text="Bem-vindo à Página 3"
            FontSize="30"
            HorizontalOptions="Center" />

        <Button
            Text="Voltar"
            HorizontalOptions="End"
            Clicked="Button_Clicked" />

    </VerticalStackLayout>

</ContentPage>
```

---

# 7. Page3.xaml.cs

Na terceira página usamos o `PopAsync()`.

```csharp
namespace AppNavigationPage;

public partial class Page3 : ContentPage
{
    public Page3()
    {
        InitializeComponent();
    }

    private async void Button_Clicked(object sender, EventArgs e)
    {
        await Navigation.PopAsync();
    }
}
```

O comando:

```csharp
await Navigation.PopAsync();
```

remove a página atual da pilha e retorna para a página anterior.

Antes:

```text
Page1
Page2
Page3 ← atual
```

Depois:

```text
Page1
Page2 ← atual
```

---

# 8. Funcionamento da NavigationPage

O funcionamento pode ser entendido como uma pilha.

### Primeiro momento

```text
Page1
```

### Depois de executar PushAsync(Page2)

```text
Page1
Page2 ← atual
```

### Depois de executar PushAsync(Page3)

```text
Page1
Page2
Page3 ← atual
```

### Depois de executar PopAsync()

```text
Page1
Page2 ← atual
```

---

# 9. Principais propriedades e métodos utilizados

|Propriedade/Método|Função|
|---|---|
|`Title`|Define o título da página|
|`Padding`|Define o espaçamento interno|
|`Text`|Define o texto de um controle|
|`FontSize`|Define o tamanho da fonte|
|`HorizontalOptions`|Define o alinhamento horizontal|
|`Clicked`|Define o evento de clique|
|`NavigationPage`|Gerencia a navegação|
|`Navigation`|Acessa o sistema de navegação|
|`PushAsync()`|Adiciona uma nova página à pilha|
|`PopAsync()`|Remove a página atual|
|`async`|Permite trabalhar com operações assíncronas|
|`await`|Aguarda a conclusão da operação|

---

# 10. Fluxo completo

O fluxo da aplicação é:

```text
                    NavigationPage
                          |
                          v
                       Page1
                          |
                    PushAsync()
                          |
                          v
                       Page2
                          |
                    PushAsync()
                          |
                          v
                       Page3
                          |
                     PopAsync()
                          |
                          v
                       Page2
```

## Resumo

A `NavigationPage` é responsável por controlar a navegação entre diferentes `ContentPage`.

A navegação funciona utilizando uma pilha de páginas.

`PushAsync()` adiciona uma nova página à pilha.

`PopAsync()` remove a página atual e retorna para a página anterior.

A propriedade `Title` permite definir o título da página na barra de navegação.

O evento `Clicked` permite executar uma ação quando o usuário pressiona um botão.

A estrutura básica utilizada na aula pode ser resumida assim:

```text
ContentPage = tela da aplicação

NavigationPage = mecanismo de navegação

PushAsync() = avançar para outra página

PopAsync() = voltar para a página anterior

Title = título da página

Clicked = evento executado ao clicar

Navigation = acesso ao mecanismo de navegação
```