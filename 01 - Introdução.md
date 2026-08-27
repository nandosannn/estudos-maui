# 📑 Índice

1. [[#01. O que é .NET MAUI]]
2. [[#02. .NET MAUI vs Xamarin.Forms vs Desenvolvimento Nativo]]
3. [[#03. Desenvolvimento Multiplataforma]]
4. [[#04. Estrutura de um Projeto .NET MAUI]]
5. [[#05. MauiProgram.cs]]
6. [[#06. App.xaml e App.xaml.cs]]
7. [[#07. AppShell.xaml e AppShell.xaml.cs]]
8. [[#08. MainPage.xaml]]
9. [[#09. Code-behind (.xaml.cs)]]
10. [[#10. XAML]]
11. [[#11. Pasta Platforms]]
12. [[#12. Pasta Resources]]
13. [[#13. Ciclo de Vida da Aplicação]]
14. [[#14. Fluxo de Inicialização do MAUI]]
15. [[#15. Resumo para Concursos]]


# .NET MAUI — Fundamentos

O **.NET MAUI (Multi-platform App UI)** é um framework da Microsoft para desenvolvimento de aplicações com **C# e .NET**, permitindo criar um único projeto capaz de gerar aplicações para diferentes plataformas.

A ideia central é:

> **Escrever a maior parte do código uma vez e executar a aplicação em diferentes sistemas operacionais.**

As principais plataformas são:

- 🤖 Android
- 🍎 iOS
- 🪟 Windows
- 🍎 macOS, através do **MacCatalyst**

---

# 1. O que é .NET MAUI?

**.NET MAUI** significa:

> **.NET Multi-platform App UI**

É uma evolução do **Xamarin.Forms**, integrada ao ecossistema moderno do .NET.

Com MAUI, podemos desenvolver:

```
                 Aplicação .NET MAUI
                         │
             ┌───────────┼───────────┐
             │           │           │
          Android       iOS       Windows
                                     │
                                  MacCatalyst
```

O desenvolvedor utiliza principalmente:

- **C#** → lógica da aplicação
- **XAML** → construção das interfaces
- **.NET** → runtime e bibliotecas
- **MAUI** → abstração da interface multiplataforma

Por exemplo, podemos criar:

```
<Label
    Text="Olá, mundo!"
    FontSize="30"
    HorizontalOptions="Center" />
```

Essa mesma definição de interface pode ser utilizada para diferentes plataformas.

### Por que isso é importante?

Sem uma solução multiplataforma, poderíamos precisar criar:

```
Android → Kotlin/Java
iOS → Swift/Objective-C
Windows → C#/C++/WinUI
macOS → Swift/Objective-C
```

Com MAUI:

```
                C# + XAML
                    │
                 .NET MAUI
          ┌─────────┼─────────┐
          ↓         ↓         ↓
       Android     iOS     Windows
                              ↓
                         MacCatalyst
```

Isso reduz a quantidade de código específico necessário para cada plataforma.

---

# 2. .NET MAUI × Xamarin.Forms × Desenvolvimento Nativo

Essa comparação é muito importante.

## Desenvolvimento nativo

No desenvolvimento nativo, normalmente usamos a tecnologia específica de cada sistema.

|Plataforma|Tecnologias tradicionais|
|---|---|
|Android|Kotlin / Java|
|iOS|Swift / Objective-C|
|Windows|C# / C++ + WinUI|
|macOS|Swift / Objective-C|

Cada plataforma possui suas próprias APIs, ferramentas e componentes.

Por exemplo:

```
Aplicativo Android
        ↓
Código Android específico

Aplicativo iOS
        ↓
Código iOS específico
```

Consequentemente, uma empresa que queira desenvolver para Android e iOS pode precisar manter dois projetos diferentes.

---

# 3. Xamarin.Forms

O **Xamarin.Forms** foi uma das principais tecnologias utilizadas para criar interfaces multiplataforma utilizando C#.

A ideia era semelhante:

```
             Xamarin.Forms
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
     Android                iOS
```

O desenvolvedor criava uma interface compartilhada e o Xamarin fazia a ponte para os controles nativos.

Porém, o Xamarin fazia parte da geração anterior do ecossistema .NET.

O **.NET MAUI é o sucessor do Xamarin.Forms**.

A Microsoft encerrou o suporte ao Xamarin em **1º de maio de 2024**, tornando o MAUI a opção moderna dentro desse ecossistema.

---

# 4. .NET MAUI × Xamarin.Forms

Podemos pensar na evolução assim:

```
Xamarin
   │
   └── Xamarin.Forms
           │
           ↓
       .NET MAUI
```

O MAUI trouxe uma arquitetura mais integrada ao .NET moderno.

Algumas diferenças importantes:

|Xamarin.Forms|.NET MAUI|
|---|---|
|Ecossistema Xamarin|Ecossistema .NET|
|Projeto multiplataforma|Projeto multiplataforma|
|C# + XAML|C# + XAML|
|Estrutura de projeto mais separada|Projeto único|
|Antecessor|Sucessor|
|Suporte encerrado|Tecnologia moderna|

---

# 5. Multiplataforma

Uma das principais características do MAUI é o desenvolvimento multiplataforma.

O mesmo projeto pode possuir:

```
MeuAplicativo
│
├── Android
├── iOS
├── MacCatalyst
└── Windows
```

Porém, isso **não significa que absolutamente tudo será idêntico em todas as plataformas**.

Esse é um conceito muito importante.

O MAUI tenta fornecer uma abstração comum, mas cada sistema operacional possui suas próprias características.

Por exemplo:

```
                Button
                  │
          .NET MAUI Button
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
    Android      iOS      Windows
       ↓          ↓          ↓
 Controle      Controle   Controle
   nativo       nativo     nativo
```

Por isso, o mesmo componente pode apresentar pequenas diferenças visuais ou comportamentais dependendo da plataforma.

Isso é algo que você já encontrou nos seus estudos de MAUI: **um componente pode funcionar ou apresentar uma aparência diferente no Windows e no Android**.

---

# 6. Estrutura de um projeto .NET MAUI

Quando criamos um projeto MAUI, encontramos uma estrutura semelhante a:

```
MeuApp/
│
├── Platforms/
│   ├── Android/
│   ├── iOS/
│   ├── MacCatalyst/
│   └── Windows/
│
├── Resources/
│   ├── AppIcon/
│   ├── Fonts/
│   ├── Images/
│   ├── Raw/
│   ├── Splash/
│   └── Styles/
│
├── App.xaml
├── App.xaml.cs
├── AppShell.xaml
├── AppShell.xaml.cs
├── MainPage.xaml
├── MainPage.xaml.cs
├── MauiProgram.cs
└── MeuApp.csproj
```

Cada arquivo possui uma responsabilidade.

Podemos visualizar o fluxo básico:

```
MauiProgram.cs
       ↓
      App
       ↓
   AppShell
       ↓
   MainPage
       ↓
MainPage.xaml
       +
MainPage.xaml.cs
```

Agora vamos entender cada um.

---

# 7. MauiProgram.cs

O arquivo:

```
MauiProgram.cs
```

é responsável principalmente pela **configuração e inicialização da aplicação MAUI**.

Ele contém o método:

```
public static MauiApp CreateMauiApp()
```

Um exemplo simplificado:

```
public static MauiApp CreateMauiApp()
{
    var builder = MauiApp.CreateBuilder();

    builder
        .UseMauiApp<App>();

    return builder.Build();
}
```

Observe:

```
MauiApp.CreateBuilder()
```

Cria o **builder** utilizado para configurar a aplicação.

Depois:

```
.UseMauiApp<App>()
```

indica qual classe representa a aplicação principal.

Finalmente:

```
builder.Build()
```

constrói a aplicação.

---

## O que mais pode ser configurado no MauiProgram?

Muita coisa.

Por exemplo:

### Fontes

```
.ConfigureFonts(fonts =>
{
    fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
});
```

### Injeção de dependência

```
builder.Services.AddSingleton<ApiService>();
```

### Serviços

```
builder.Services.AddTransient<LoginPage>();
```

### Bibliotecas e frameworks

Também podemos registrar componentes externos.

Portanto, uma boa forma de memorizar é:

> **MauiProgram.cs = configuração e inicialização da aplicação.**

---

# 8. App.xaml

O:

```
App.xaml
```

é utilizado para definir **recursos globais da aplicação**.

Por exemplo:

```
<Application
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuApp.App">

    <Application.Resources>

        <Style TargetType="Label">
            <Setter Property="FontSize" Value="20" />
        </Style>

    </Application.Resources>

</Application>
```

Nesse exemplo, estamos definindo um estilo que pode ser utilizado globalmente.

Podemos colocar nele:

- estilos;
- cores;
- recursos;
- templates;
- configurações visuais reutilizáveis.

---

# 9. App.xaml.cs

É o **code-behind** do `App.xaml`.

Normalmente encontramos:

```
public partial class App : Application
{
    public App()
    {
        InitializeComponent();

        MainPage = new AppShell();
    }
}
```

Aqui temos algo extremamente importante:

```
MainPage = new AppShell();
```

Isso determina a página inicial da aplicação.

O fluxo será:

```
App
 ↓
AppShell
 ↓
Página inicial
```

### `InitializeComponent()`

Esse método:

```
InitializeComponent();
```

inicializa os elementos definidos no XAML associado.

Ou seja:

```
App.xaml
   ↕
App.xaml.cs
```

O XAML define a estrutura/recursos, enquanto o `.cs` contém lógica relacionada à classe.

---

# 10. AppShell.xaml

O `AppShell` representa a estrutura de **navegação da aplicação**.

Por exemplo:

```
<Shell
    x:Class="MeuApp.AppShell"
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml">

    <ShellContent
        Title="Início"
        ContentTemplate="{DataTemplate local:MainPage}" />

</Shell>
```

Podemos pensar no Shell como uma espécie de **gerenciador de navegação**.

Ele pode trabalhar com:

- páginas;
- rotas;
- abas;
- menus;
- navegação;
- Flyout.

Por exemplo:

```
             AppShell
                │
       ┌────────┼────────┐
       ↓        ↓        ↓
     Home    Produtos   Perfil
```

---

# 11. Shell e navegação

Uma das grandes vantagens do Shell é facilitar a navegação.

Podemos registrar uma rota:

```
Routing.RegisterRoute(
    "detalhes",
    typeof(DetalhesPage)
);
```

E navegar:

```
await Shell.Current.GoToAsync("detalhes");
```

Podemos passar parâmetros:

```
await Shell.Current.GoToAsync(
    $"detalhes?id={10}"
);
```

Então:

```
Página A
   │
   │ GoToAsync()
   ↓
Página B
```

---

# 12. MainPage.xaml

Esse é um dos arquivos mais importantes para quem está começando.

O:

```
MainPage.xaml
```

normalmente representa a **interface visual de uma página**.

Exemplo:

```
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuApp.MainPage">

    <VerticalStackLayout
        Padding="30"
        Spacing="20">

        <Label
            Text="Olá, mundo!"
            FontSize="30" />

        <Button
            Text="Clique aqui" />

    </VerticalStackLayout>

</ContentPage>
```

Aqui estamos definindo a interface.

Temos:

```
ContentPage
    │
    └── VerticalStackLayout
            │
            ├── Label
            │
            └── Button
```

---

# 13. XAML

O XAML é uma linguagem baseada em XML utilizada para **declarar a interface**.

Por exemplo:

```
<Label Text="Olá!" />
```

é uma maneira declarativa de dizer:

> Quero uma Label cujo texto seja "Olá!".

Isso é diferente de construir tudo diretamente em C#.

Em C# poderíamos fazer algo semelhante a:

```
var label = new Label
{
    Text = "Olá!"
};
```

Enquanto no XAML:

```
<Label Text="Olá!" />
```

O XAML geralmente torna a construção da interface mais organizada e legível.

---

# 14. MainPage.xaml.cs

Esse arquivo é chamado de **code-behind**.

Temos:

```
MainPage.xaml
       ↕
MainPage.xaml.cs
```

O XAML cuida principalmente da interface.

O `.xaml.cs` contém a lógica relacionada àquela interface.

Por exemplo:

```
public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
    }

    private void Button_Clicked(
        object sender,
        EventArgs e)
    {
        DisplayAlert(
            "Aviso",
            "Botão clicado!",
            "OK");
    }
}
```

No XAML:

```
<Button
    Text="Clique aqui"
    Clicked="Button_Clicked" />
```

Temos:

```
Usuário clica
      ↓
Button
      ↓
Clicked
      ↓
Button_Clicked()
      ↓
Código C#
```

---

# 15. O que é Code-behind?

**Code-behind** é o código associado a um arquivo XAML.

Exemplo:

```
MainPage.xaml
      +
MainPage.xaml.cs
      ↓
    MainPage
```

O XAML representa principalmente a **estrutura visual**.

O `.xaml.cs` contém a **lógica da página**.

### Porém, atenção

Em aplicações MAUI maiores, não é recomendado colocar toda a lógica da aplicação no code-behind.

Normalmente utilizamos arquiteturas como:

```
View
 ↓
ViewModel
 ↓
Service
 ↓
API / Banco
```

especialmente com **MVVM**.

Para aprender MAUI, entretanto, o code-behind é fundamental porque ajuda a entender a relação entre interface e lógica.

---

# 16. Ciclo de vida básico da aplicação

Outro conceito importante é o **ciclo de vida**.

Uma aplicação passa por diferentes estados.

Podemos simplificar:

```
       Aplicação iniciada
              ↓
           Criada
              ↓
            Ativa
              ↓
          Background
              ↓
       Volta para ativa
              ↓
          Encerrada
```

No MAUI, a classe `Window` possui eventos importantes relacionados ao ciclo de vida.

Por exemplo:

```
protected override Window CreateWindow(
    IActivationState? activationState)
{
    return new Window(new AppShell());
}
```

A aplicação cria uma janela que contém o `AppShell`.

---

# 17. Eventos do ciclo de vida

Podemos trabalhar com eventos como:

```
Created
Activated
Deactivated
Stopped
Resumed
Destroying
```

A ideia geral é:

### Created

A janela/aplicação foi criada.

```
Aplicação → criada
```

### Activated

A aplicação está ativa.

```
Aplicação → usuário está interagindo
```

### Deactivated

A aplicação deixa de estar ativa.

```
Aplicação → perdeu foco
```

### Stopped

A aplicação deixou de estar em execução ativa.

### Resumed

A aplicação retorna para o estado ativo.

```
Background
    ↓
Resumed
    ↓
Foreground
```

### Destroying

A janela está sendo destruída.

---

# 18. Um detalhe importante: ciclo de vida não é igual em todas as plataformas

Como MAUI é multiplataforma, o comportamento do ciclo de vida pode variar entre:

```
Android
iOS
Windows
MacCatalyst
```

Isso acontece porque cada sistema operacional possui seu próprio modelo de ciclo de vida.

Por isso, o MAUI fornece uma abstração comum, mas determinadas situações ainda exigem código específico da plataforma.

---

# 19. Onde entra a pasta Platforms?

A pasta:

```
Platforms/
```

é utilizada quando precisamos de código ou configuração **específica de determinada plataforma**.

Temos:

```
Platforms/
├── Android/
├── iOS/
├── MacCatalyst/
└── Windows/
```

Por exemplo:

```
Código compartilhado
        │
        ├── Android específico
        ├── iOS específico
        ├── Windows específico
        └── MacCatalyst específico
```

Isso é uma das grandes ideias do MAUI:

> **Compartilhar o máximo possível, mas permitir código específico quando necessário.**

---

# 20. Como tudo se conecta?

Esse é provavelmente o modelo mais importante para você memorizar:

```
                    MauiProgram.cs
                         │
                         │ configura
                         ↓
                       App
                         │
                         │ inicializa
                         ↓
                     AppShell
                         │
                         │ navegação
                         ↓
                     MainPage
                    ┌────┴────┐
                    ↓         ↓
             MainPage.xaml   .xaml.cs
                    │         │
                    │         │
                 Interface   Lógica
```

Podemos expandir:

```
                       .NET MAUI
                           │
              ┌────────────┴────────────┐
              │                         │
        Código compartilhado       Código específico
              │                         │
              │                     Platforms/
              │                    ┌────┼────┐
              │                    ↓    ↓    ↓
              │                 Android iOS Windows
              │
       ┌──────┴──────┐
       ↓             ↓
      XAML          C#
       │             │
       ↓             ↓
  Interface       Lógica
       │             │
       └──────┬──────┘
              ↓
            App
              ↓
          AppShell
              ↓
           Páginas
```

---

# 21. Resumo para concursos/provas

|Conceito|Função|
|---|---|
|**.NET MAUI**|Framework multiplataforma para .NET|
|**Xamarin.Forms**|Antecessor do .NET MAUI|
|**Desenvolvimento nativo**|Código específico para cada plataforma|
|**MauiProgram.cs**|Configuração e inicialização da aplicação|
|**App.xaml**|Recursos e estilos globais|
|**App.xaml.cs**|Código associado ao `App.xaml`|
|**AppShell.xaml**|Estrutura de navegação da aplicação|
|**MainPage.xaml**|Interface visual de uma página|
|**MainPage.xaml.cs**|Code-behind da página|
|**Platforms/**|Código/configuração específica de plataforma|
|**Resources/**|Imagens, fontes, ícones, splash etc.|
|**XAML**|Linguagem declarativa para interfaces|
|**C#**|Lógica da aplicação|
|**Code-behind**|Código associado ao XAML|
|**Shell**|Navegação e estrutura da aplicação|

## 🧠 Mnemônico

Pense no MAUI assim:

> **MauiProgram configura → App inicia → Shell navega → Page apresenta → XAML desenha → C# executa.**

Ou, em uma linha:

```
MauiProgram → App → AppShell → Page → XAML + C#
```

Essa sequência é uma das melhores formas de organizar mentalmente a arquitetura básica de um projeto MAUI.