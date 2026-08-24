# FlyoutPage — Criação de menu lateral no .NET MAUI

## 1. O que é uma FlyoutPage?

A `FlyoutPage` é um tipo de página utilizado para criar um **menu lateral** em aplicativos.

Ela é muito útil quando o aplicativo possui várias funcionalidades ou várias áreas que podem ser acessadas pelo usuário.

Um exemplo comum é:

```text
┌───────────────────────────────┐
│ ☰                             │
│                               │
│       Conteúdo principal      │
│                               │
│                               │
└───────────────────────────────┘
```

Ao abrir o menu:

```text
┌──────────────┬────────────────┐
│ MENU         │                │
│              │                │
│ Página 1     │ Conteúdo       │
│ Página 2     │ principal      │
│ Página 3     │                │
│ Configurações│                │
│              │                │
└──────────────┴────────────────┘
```

A ideia principal da `FlyoutPage` é dividir a interface em duas partes:

1. **Flyout** → menu lateral.
    
2. **Detail** → conteúdo principal.
    

---

# 2. FlyoutPage x navegação por abas

Existem diferentes maneiras de organizar a navegação de um aplicativo.

Uma delas é utilizar abas, normalmente posicionadas na parte inferior:

```text
┌───────────────────────────────┐
│                               │
│       Conteúdo                │
│                               │
├───────────────────────────────┤
│ Início │ Busca │ Perfil │ ... │
└───────────────────────────────┘
```

As abas são interessantes quando temos uma quantidade relativamente pequena de funcionalidades principais.

Quando o aplicativo possui muitas opções, um menu lateral pode ser mais adequado.

Nesse caso podemos utilizar uma `FlyoutPage`.

Uma comparação simples:

|Estrutura|Característica|
|---|---|
|Abas|Boa para poucas opções principais|
|FlyoutPage|Boa para várias opções e funcionalidades|
|Flyout|Menu lateral|
|Detail|Conteúdo principal|

---

# 3. Criando o projeto

Na aula foi criado um novo projeto .NET MAUI para demonstrar a `FlyoutPage`.

O projeto utilizado na aula foi chamado de:

```text
AppFlyOutPage
```

A partir desse projeto, foram criadas as páginas que seriam utilizadas no exemplo.

---

# 4. Criando as páginas de conteúdo

Foram criadas três `ContentPage`:

```text
Page1.xaml
Page2.xaml
Page3.xaml
```

Cada uma representa uma página que poderá ser apresentada no conteúdo principal do aplicativo.

Para facilitar a identificação durante os testes, cada página recebeu um texto indicando seu nome.

Por exemplo:

```xml
<Label
    Text="Página 1"
    FontSize="48" />
```

Na Página 2:

```xml
<Label
    Text="Página 2"
    FontSize="48" />
```

E na Página 3:

```xml
<Label
    Text="Página 3"
    FontSize="48" />
```

Dessa maneira, podemos identificar visualmente qual página está sendo exibida.

---

# 5. Criando o menu

Além das três páginas de conteúdo, precisamos criar uma página que representará o nosso menu lateral.

Essa página também pode ser uma `ContentPage`.

Foi criada uma página chamada:

```text
MenuPage.xaml
```

Inicialmente podemos colocar apenas um texto para identificar o menu:

```xml
<Label
    Text="Menu"
    FontSize="48" />
```

Também podemos alterar o fundo da página para facilitar a visualização:

```xml
<ContentPage
    BackgroundColor="LightGray">
```

O menu pode ser totalmente personalizado.

Podemos colocar nele:

- Botões;
    
- Labels;
    
- Imagens;
    
- Ícones;
    
- Listas;
    
- Links;
    
- Opções de navegação;
    
- Outros componentes do .NET MAUI.
    

Portanto, o menu lateral não possui uma aparência obrigatória.

---

# 6. Estrutura da FlyoutPage

Agora temos:

```text
Page1
Page2
Page3
MenuPage
```

Porém, ainda precisamos criar a estrutura que irá juntar o menu e o conteúdo principal.

A `FlyoutPage` possui duas partes principais:

```text
FlyoutPage
├── Flyout
│   └── MenuPage
│
└── Detail
    └── Page1
```

O conceito é:

### Flyout

É a página que representa o menu lateral.

```text
Flyout → MenuPage
```

### Detail

É a página que representa o conteúdo principal.

```text
Detail → Page1
```

---

# 7. Criando a FlyoutPage manualmente

Um ponto importante apresentado na aula é que nem sempre encontramos um template específico para criar diretamente uma `FlyoutPage` no Visual Studio.

Podemos criar uma `ContentPage` normalmente e depois alterar sua classe base para `FlyoutPage`.

Por exemplo, podemos criar:

```text
FlyoutPageMenu.xaml
```

Inicialmente o Visual Studio pode criar:

```csharp
public partial class FlyoutPageMenu : ContentPage
{
    public FlyoutPageMenu()
    {
        InitializeComponent();
    }
}
```

Mas queremos que essa classe seja uma `FlyoutPage`.

Então alteramos:

```csharp
public partial class FlyoutPageMenu : FlyoutPage
{
    public FlyoutPageMenu()
    {
        InitializeComponent();
    }
}
```

Agora a classe passa a herdar de:

```csharp
FlyoutPage
```

em vez de:

```csharp
ContentPage
```

---

# 8. Alterando o XAML para FlyoutPage

Também precisamos alterar o elemento principal do arquivo XAML.

Antes:

```xml
<ContentPage
    ...
>
```

Depois:

```xml
<FlyoutPage
    ...
>
```

E precisamos informar o namespace correspondente ao projeto.

Por exemplo:

```xml
xmlns:local="clr-namespace:AppFlyOutPage"
```

O namespace deve corresponder ao namespace utilizado no projeto.

---

# 9. Flyout e Detail

A `FlyoutPage` possui duas propriedades fundamentais:

```text
Flyout
Detail
```

Elas representam as duas partes principais da estrutura.

Podemos visualizar:

```text
FlyoutPage
│
├── Flyout
│     └── Menu
│
└── Detail
      └── Página principal
```

### Flyout

Define qual página será utilizada como menu lateral.

### Detail

Define qual página será apresentada como conteúdo principal.

---

# 10. Configurando o Flyout

No XAML podemos definir a página do menu através da propriedade:

```xml
FlyoutPage.Flyout
```

Por exemplo:

```xml
<FlyoutPage.Flyout>
    <local:MenuPage />
</FlyoutPage.Flyout>
```

Nesse caso, estamos dizendo:

> A página `MenuPage` será utilizada como o menu lateral.

---

# 11. Configurando o Detail

Da mesma forma, podemos definir a página principal através de:

```xml
<FlyoutPage.Detail>
```

Por exemplo:

```xml
<FlyoutPage.Detail>
    <local:Page1 />
</FlyoutPage.Detail>
```

Isso significa:

> A `Page1` será apresentada como o conteúdo principal da `FlyoutPage`.

---

# 12. Exemplo completo da FlyoutPage

Um exemplo simplificado da estrutura seria:

```xml
<?xml version="1.0" encoding="utf-8" ?>

<FlyoutPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    xmlns:local="clr-namespace:AppFlyOutPage"
    x:Class="AppFlyOutPage.FlyoutPageMenu">

    <FlyoutPage.Flyout>
        <local:MenuPage />
    </FlyoutPage.Flyout>

    <FlyoutPage.Detail>
        <local:Page1 />
    </FlyoutPage.Detail>

</FlyoutPage>
```

Essa estrutura estabelece:

```text
FlyoutPageMenu
│
├── Flyout
│   └── MenuPage
│
└── Detail
    └── Page1
```

---

# 13. Por que precisamos do namespace?

Para utilizar páginas criadas no próprio projeto dentro do XAML, precisamos informar ao XAML onde essas classes estão localizadas.

Por isso utilizamos:

```xml
xmlns:local="clr-namespace:AppFlyOutPage"
```

Depois podemos utilizar:

```xml
<local:MenuPage />
```

e:

```xml
<local:Page1 />
```

O prefixo `local` é apenas um nome que escolhemos para representar o namespace.

Por exemplo:

```xml
xmlns:local="clr-namespace:AppFlyOutPage"
```

significa que:

```text
local
```

representa:

```text
AppFlyOutPage
```

Então:

```xml
<local:Page1 />
```

significa:

> Use a classe `Page1` pertencente ao namespace `AppFlyOutPage`.

---

# 14. FlyoutPage não recebe conteúdo diretamente como ContentPage

Uma diferença importante entre `ContentPage` e `FlyoutPage` é a maneira como o conteúdo é organizado.

Uma `ContentPage` normalmente recebe diretamente seu conteúdo:

```xml
<ContentPage>

    <VerticalStackLayout>
        ...
    </VerticalStackLayout>

</ContentPage>
```

Já a `FlyoutPage` trabalha com suas duas áreas principais:

```text
Flyout
Detail
```

Portanto, a estrutura é organizada dessa maneira:

```xml
<FlyoutPage>

    <FlyoutPage.Flyout>
        ...
    </FlyoutPage.Flyout>

    <FlyoutPage.Detail>
        ...
    </FlyoutPage.Detail>

</FlyoutPage>
```

---

# 15. Configurando o App

Depois de criar a `FlyoutPage`, precisamos fazer com que ela seja a página inicial do aplicativo.

No arquivo `App.xaml.cs`, podemos alterar a página principal.

Por exemplo:

```csharp
public partial class App : Application
{
    public App()
    {
        InitializeComponent();

        MainPage = new FlyoutPageMenu();
    }
}
```

Assim, quando o aplicativo iniciar, a primeira página será:

```text
FlyoutPageMenu
```

Em versões mais recentes do .NET MAUI, dependendo da estrutura do projeto, a inicialização da janela também pode ser feita através de `CreateWindow`.

O importante é que a `FlyoutPage` seja utilizada como a raiz da interface que será apresentada.

---

# 16. Estrutura final do projeto

Depois das alterações, podemos ter uma estrutura semelhante a:

```text
AppFlyOutPage
│
├── App.xaml
├── App.xaml.cs
│
├── Page1.xaml
├── Page1.xaml.cs
│
├── Page2.xaml
├── Page2.xaml.cs
│
├── Page3.xaml
├── Page3.xaml.cs
│
├── MenuPage.xaml
├── MenuPage.xaml.cs
│
├── FlyoutPageMenu.xaml
└── FlyoutPageMenu.xaml.cs
```

A responsabilidade de cada página é:

|Arquivo|Responsabilidade|
|---|---|
|`Page1`|Primeiro conteúdo|
|`Page2`|Segundo conteúdo|
|`Page3`|Terceiro conteúdo|
|`MenuPage`|Menu lateral|
|`FlyoutPageMenu`|Estrutura que une menu e conteúdo|
|`App`|Inicialização do aplicativo|

---

# 17. Como funciona visualmente

Quando o aplicativo é executado, temos inicialmente:

```text
┌─────────────────────────────────┐
│ ☰                               │
│                                 │
│                                 │
│          Página 1               │
│                                 │
│                                 │
└─────────────────────────────────┘
```

A Página 1 é o `Detail`.

Quando o usuário abre o menu:

```text
┌──────────────┬──────────────────┐
│              │                  │
│    MENU      │    Página 1      │
│              │                  │
│              │                  │
│              │                  │
└──────────────┴──────────────────┘
```

O lado esquerdo representa o `Flyout`.

O lado direito representa o `Detail`.

---

# 18. Comportamento no Windows e no celular

O comportamento visual da `FlyoutPage` pode variar de acordo com a plataforma.

No Windows, o menu lateral pode aparecer de uma maneira mais aberta ou visível.

Em dispositivos móveis, como Android, normalmente o menu fica inicialmente escondido e pode ser aberto pelo usuário.

Podemos imaginar:

### Menu fechado

```text
┌─────────────────────────┐
│ ☰                       │
│                         │
│       Página 1          │
│                         │
└─────────────────────────┘
```

### Menu aberto

```text
┌─────────────┬───────────┐
│ MENU        │ Página 1  │
│             │           │
│ Página 1    │           │
│ Página 2    │           │
│ Página 3    │           │
└─────────────┴───────────┘
```

---

# 19. O menu pode controlar o Detail

Nesta primeira parte da aula, o menu foi criado apenas como estrutura visual.

Posteriormente, podemos colocar elementos interativos dentro dele, como:

```text
MENU

[ Página 1 ]

[ Página 2 ]

[ Página 3 ]

[ Configurações ]

[ Sobre ]
```

Cada opção poderá alterar a propriedade:

```csharp
Detail
```

Por exemplo:

```csharp
Detail = new Page2();
```

Isso faria com que a Página 2 passasse a ser apresentada como conteúdo principal.

Portanto, o funcionamento pode ser:

```text
Usuário clica em "Página 2"
              ↓
       Menu executa ação
              ↓
     Detail = new Page2()
              ↓
       Página 2 aparece
```

---

# 20. Conceito central da FlyoutPage

A ideia mais importante da aula é entender que a `FlyoutPage` funciona como um **container de navegação dividido em duas partes**:

```text
             FlyoutPage
                 │
       ┌─────────┴─────────┐
       ↓                   ↓
    Flyout               Detail
       │                   │
       ↓                   ↓
     Menu              Conteúdo
```

O `Flyout` representa o menu lateral.

O `Detail` representa a página que está sendo exibida.

Essa estrutura permite criar aplicativos com muitas funcionalidades sem precisar colocar todas elas em uma barra de abas.

---

# 21. Comparação com NavigationPage

A `NavigationPage` e a `FlyoutPage` possuem objetivos diferentes.

### NavigationPage

É utilizada principalmente para navegação sequencial:

```text
Página 1
   ↓
Página 2
   ↓
Página 3
```

Utilizamos métodos como:

```csharp
PushAsync()
PopAsync()
PopToRootAsync()
```

### FlyoutPage

É utilizada principalmente para apresentar um menu lateral:

```text
             FlyoutPage
             /         \
          Menu        Conteúdo
```

O usuário pode utilizar o menu para escolher diferentes áreas do aplicativo.

---

# 22. Resumo da aula

Nesta aula aprendi o conceito e a estrutura básica da `FlyoutPage` no .NET MAUI.

Os principais conceitos são:

- `FlyoutPage` representa uma estrutura com menu lateral.
    
- O `Flyout` representa o menu.
    
- O `Detail` representa o conteúdo principal.
    
- O menu também pode ser uma `ContentPage`.
    
- A aparência do menu pode ser totalmente personalizada.
    
- A `FlyoutPage` pode ser criada manualmente a partir de uma `ContentPage`.
    
- É necessário alterar a herança da classe para `FlyoutPage`.
    
- Também é necessário alterar o elemento principal do XAML para `FlyoutPage`.
    
- Podemos utilizar `FlyoutPage.Flyout` para definir o menu.
    
- Podemos utilizar `FlyoutPage.Detail` para definir o conteúdo principal.
    
- O `xmlns` permite acessar páginas e classes do próprio projeto pelo XAML.
    
- A `FlyoutPage` pode ser definida como a página inicial do aplicativo.
    
- Em dispositivos móveis, o menu normalmente começa fechado.
    
- O menu pode posteriormente receber botões ou outros controles para alterar o conteúdo do `Detail`.
    

A estrutura fundamental é:

```xml
<FlyoutPage>

    <FlyoutPage.Flyout>
        <local:MenuPage />
    </FlyoutPage.Flyout>

    <FlyoutPage.Detail>
        <local:Page1 />
    </FlyoutPage.Detail>

</FlyoutPage>
```

Podemos resumir:

```text
FlyoutPage
│
├── Flyout → Menu lateral
│
└── Detail → Conteúdo principal
```

O ponto mais importante é lembrar que **a `FlyoutPage` não é o próprio menu**. Ela é a estrutura que organiza o **menu lateral (`Flyout`)** e o **conteúdo principal (`Detail`)**.

# 22. Código

## `FlyoutPageMenu.xaml`

```xml
<?xml version="1.0" encoding="utf-8" ?>
<FlyoutPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
            xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
            xmlns:pages="clr-namespace:AppFlyoutPage"
            x:Class="AppFlyoutPage.FlyoutPageMenu"
            Title="FlyoutPageMenu">
    <FlyoutPage.Flyout>
        <!-- Página de Menu-->
        <pages:Menu />
    </FlyoutPage.Flyout>
    <FlyoutPage.Detail>
        <!-- Página de conteúdo central-->

        <NavigationPage>
            <x:Arguments>
                <pages:Page1 />
            </x:Arguments>
        </NavigationPage>
        
    </FlyoutPage.Detail>
</FlyoutPage>
```

## `FlyoutPageMenu.xaml.cs`

```C#
namespace AppFlyoutPage;

public partial class FlyoutPageMenu : FlyoutPage
{
	public FlyoutPageMenu()
	{
		InitializeComponent();
	}
}
```

## `Menu.xaml`

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="AppFlyoutPage.Menu"
             Title="Menu"
             BackgroundColor="LightGray">
    <VerticalStackLayout>
        <Label 
            Text="Menu"
            FontSize="48"
            VerticalOptions="Center" 
            HorizontalOptions="Center" />

        <Button Text="Página 1" BackgroundColor="Transparent" TextColor="Black" Clicked="OnButtonClickedPage1" />
        <Button Text="Página 2" BackgroundColor="Transparent" TextColor="Black" Clicked="OnButtonClickedPage2"/>
        <Button Text="Página 3" BackgroundColor="Transparent" TextColor="Black" Clicked="OnButtonClickedPage3"/>
    </VerticalStackLayout>
</ContentPage>
```

## `Menu.xaml.cs`

```C#
namespace AppFlyoutPage;

public partial class Menu : ContentPage
{
	public Menu()
	{
		InitializeComponent();
	}

    private void OnButtonClickedPage1(object sender, EventArgs e)
    {
        ((FlyoutPage)App.Current.MainPage).Detail = new NavigationPage(new Page1());
    }

    private void OnButtonClickedPage2(object sender, EventArgs e)
    {
        ((FlyoutPage)App.Current.MainPage).Detail = new NavigationPage(new Page2());
    }

    private void OnButtonClickedPage3(object sender, EventArgs e)
    {
        ((FlyoutPage)App.Current.MainPage).Detail = new NavigationPage(new Page3());
    }
}
```

