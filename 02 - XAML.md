# 2. XAML no .NET MAUI 10.0.400

O **XAML (eXtensible Application Markup Language)** é a linguagem de marcação usada pelo .NET MAUI para **declarar a interface visual da aplicação**.

No MAUI 10.0.400, normalmente você encontrará arquivos como:

```
MainPage.xaml
MainPage.xaml.cs
```

O `.xaml` define a **interface**, enquanto o `.xaml.cs` contém o **Code-Behind**, ou seja, a lógica associada àquela interface.

---

# 📑 Índice

1. [[#1. O que é XAML]]
2. [[#2. Sintaxe do XAML]]
3. [[#3. Elementos e atributos]]
4. [[#4. `x Name`]]
5. Namespaces
6. Eventos
7. Propriedades
8. `StaticResource`
9. `DynamicResource`
10. Styles
11. Resources
12. Diferenças importantes
13. Quadro de revisão

---

# 1. O que é XAML

**XAML** é uma linguagem declarativa baseada em XML utilizada para definir a interface de aplicações.

No .NET MAUI, ela permite declarar:

- páginas;
- layouts;
- botões;
- textos;
- imagens;
- campos de entrada;
- cores;
- estilos;
- recursos;
- eventos;
- propriedades.

Por exemplo:

```
<VerticalStackLayout>
    <Label Text="Olá, mundo!" />
    <Button Text="Clique aqui" />
</VerticalStackLayout>
```

Esse código declara uma interface contendo um `Label` e um `Button`.

## XAML × C#

A mesma interface poderia ser construída em C#, mas o XAML torna a declaração da interface mais organizada.

### XAML

```
<VerticalStackLayout>
    <Label Text="Olá!" />
    <Button Text="Clique aqui" />
</VerticalStackLayout>
```

### C#

```
var layout = new VerticalStackLayout();

layout.Children.Add(
    new Label
    {
        Text = "Olá!"
    }
);

layout.Children.Add(
    new Button
    {
        Text = "Clique aqui"
    }
);
```

### Resumo

|Conceito|Função|
|---|---|
|XAML|Declara a interface|
|C#|Implementa lógica e comportamento|
|`.xaml`|Arquivo da interface|
|`.xaml.cs`|Code-Behind|
|XML|Base sintática do XAML|

> **Atenção para provas:** XAML **não é uma linguagem de programação tradicional**. É uma linguagem de **marcação declarativa**.

---

# 2. Sintaxe do XAML

Como XAML é baseado em XML, ele utiliza uma estrutura de **elementos**, **atributos** e **tags**.

Exemplo:

```
<Label
    Text="Olá, Fernando!"
    FontSize="24"
    HorizontalOptions="Center" />
```

Temos:

```
<Label ... />
  ↑
elemento
```

E:

```
Text="Olá, Fernando!"
```

é um atributo/propriedade.

---

## 2.1 Elemento

Um elemento representa um objeto da interface.

```
<Label />
```

Nesse caso, `Label` representa um objeto `Microsoft.Maui.Controls.Label`.

Outro exemplo:

```
<Button />
```

Representa um `Button`.

---

## 2.2 Atributo

Os atributos são utilizados para configurar propriedades.

```
<Label Text="Olá" />
```

Aqui:

```
Label
 └── Text="Olá"
```

`Text` configura a propriedade `Text`.

Outro exemplo:

```
<Button
    Text="Entrar"
    FontSize="18"
    Padding="20" />
```

|Elemento|Propriedade|Valor|
|---|---|---|
|`Button`|`Text`|`"Entrar"`|
|`Button`|`FontSize`|`18`|
|`Button`|`Padding`|`20`|

---

# 3. Elementos e atributos

Essa é uma das partes mais importantes para entender XAML.

Considere:

```
<Label Text="Olá" />
```

Podemos escrever a mesma propriedade usando **Property Element Syntax**:

```
<Label>
    <Label.Text>Olá</Label.Text>
</Label>
```

Os dois representam essencialmente a mesma configuração.

---

## 3.1 Attribute Syntax

Forma compacta:

```
<Label Text="Olá" />
```

É chamada de **Attribute Syntax**.

---

## 3.2 Property Element Syntax

Forma expandida:

```
<Label>
    <Label.Text>
        Olá
    </Label.Text>
</Label>
```

É útil quando a propriedade possui uma configuração mais complexa.

Por exemplo:

```
<Label>
    <Label.TextColor>
        Red
    </Label.TextColor>
</Label>
```

---

## 3.3 Exemplo mais complexo

```
<Button Text="Salvar">
    <Button.Background>
        <LinearGradientBrush>
            <GradientStop Color="Blue" Offset="0" />
            <GradientStop Color="Purple" Offset="1" />
        </LinearGradientBrush>
    </Button.Background>
</Button>
```

Nesse caso, seria muito difícil representar tudo adequadamente usando apenas um atributo.

---

## 3.4 Elementos podem conter outros elementos

Exemplo:

```
<VerticalStackLayout>

    <Label Text="Nome" />

    <Entry Placeholder="Digite seu nome" />

    <Button Text="Enviar" />

</VerticalStackLayout>
```

Temos uma hierarquia:

```
VerticalStackLayout
├── Label
├── Entry
└── Button
```

Isso é extremamente importante no MAUI.

---

# 4. `x:Name`

`x:Name` atribui um **nome ao elemento XAML**, permitindo que ele seja referenciado no Code-Behind.

Exemplo:

```
<Label
    x:Name="lblMensagem"
    Text="Olá!" />
```

No arquivo `.xaml.cs`:

```
lblMensagem.Text = "Mensagem alterada!";
```

---

## Exemplo completo

### MainPage.xaml

```
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuApp.MainPage">

    <VerticalStackLayout Padding="20">

        <Label
            x:Name="lblMensagem"
            Text="Valor inicial" />

        <Button
            Text="Alterar"
            Clicked="Button_Clicked" />

    </VerticalStackLayout>

</ContentPage>
```

### MainPage.xaml.cs

```
namespace MeuApp;

public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
    }

    private void Button_Clicked(object sender, EventArgs e)
    {
        lblMensagem.Text = "Valor alterado!";
    }
}
```

---

## `x:Name` × `Name`

No XAML, é comum encontrar:

```
x:Name="meuBotao"
```

O prefixo `x:` indica que `Name` pertence ao namespace XAML (`http://schemas.microsoft.com/winfx/2009/xaml`).

No MAUI, `x:Name` é a forma tradicional e explícita para nomear elementos XAML.

### Para memorizar

```
x:Name
   ↓
identifica o elemento
   ↓
permite acessá-lo no Code-Behind
```

---

# 5. Namespaces

Namespaces são utilizados para **identificar de onde vêm os tipos utilizados no XAML**.

Observe o início de uma página MAUI:

```
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuApp.MainPage">
```

Temos dois namespaces importantes.

---

## 5.1 Namespace padrão

```
xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
```

Define o namespace padrão dos controles MAUI.

Por isso podemos escrever:

```
<Label />
<Button />
<Entry />
```

sem precisar escrever um prefixo.

---

## 5.2 Namespace `x`

```
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
```

Define o prefixo `x`.

Assim podemos utilizar:

```
x:Name
x:Class
x:Key
x:TypeArguments
```

---

## 5.3 Namespace para classes próprias

Suponha que exista:

```
namespace MeuApp.Controls;

public class MeuControle : ContentView
{
}
```

No XAML:

```
xmlns:controls="clr-namespace:MeuApp.Controls"
```

Agora podemos usar:

```
<controls:MeuControle />
```

A estrutura fica:

```
xmlns:controls
      ↓
clr-namespace:MeuApp.Controls
      ↓
controls:MeuControle
```

---

## 5.4 Tabela de namespaces

|Namespace|Utilização|
|---|---|
|`xmlns`|Controles do MAUI|
|`xmlns:x`|Recursos da linguagem XAML|
|`xmlns:controls`|Classes personalizadas|
|`clr-namespace:`|Aponta para um namespace .NET|

---

# 6. Eventos

Eventos permitem executar código quando determinada ação ocorre.

Exemplos:

- botão clicado;
- texto alterado;
- página apareceu;
- propriedade modificada;
- toque realizado.

---

## 6.1 Evento `Clicked`

XAML:

```
<Button
    Text="Clique"
    Clicked="Button_Clicked" />
```

C#:

```
private void Button_Clicked(object sender, EventArgs e)
{
    DisplayAlertAsync("Aviso", "Botão clicado!", "OK");
}
```

A ligação é:

```
Clicked
   ↓
Button_Clicked
   ↓
método C#
```

---

## 6.2 Outro exemplo

```
<Entry
    Placeholder="Digite seu nome"
    TextChanged="Entry_TextChanged" />
```

C#:

```
private void Entry_TextChanged(object sender, TextChangedEventArgs e)
{
    Console.WriteLine(e.NewTextValue);
}
```

O objeto `e` contém informações sobre o evento.

---

## 6.3 Eventos comuns

|Controle|Evento|Quando ocorre|
|---|---|---|
|`Button`|`Clicked`|Botão clicado|
|`Entry`|`TextChanged`|Texto alterado|
|`CheckBox`|`CheckedChanged`|Estado alterado|
|`Switch`|`Toggled`|Switch alterado|
|`Picker`|`SelectedIndexChanged`|Seleção alterada|
|`ContentPage`|`Appearing`|Página aparece|

---

## 6.4 Eventos não são propriedades

Isso é importante:

```
<Button
    Text="OK"
    Clicked="Button_Clicked" />
```

`Text` é uma **propriedade**.

`Clicked` é um **evento**.

|`Text`|`Clicked`|
|---|---|
|Propriedade|Evento|
|Define estado/configuração|Reage a uma ação|
|`"OK"`|`Button_Clicked`|

---

# 7. Propriedades

Os controles do MAUI são objetos .NET e possuem propriedades.

Exemplo:

```
<Label
    Text="Olá"
    FontSize="24"
    TextColor="Blue"
    HorizontalOptions="Center" />
```

Aqui estamos configurando quatro propriedades:

```
Text
FontSize
TextColor
HorizontalOptions
```

---

## 7.1 Propriedades simples

```
<Label
    Text="Olá"
    FontSize="20"
    IsVisible="True"
    Opacity="0.8" />
```

|Propriedade|Tipo conceitual|Exemplo|
|---|---|---|
|`Text`|`string`|`"Olá"`|
|`FontSize`|`double`|`20`|
|`IsVisible`|`bool`|`True`|
|`Opacity`|`double`|`0.8`|

---

# 7.2 Propriedades aninhadas

Quando uma propriedade é complexa:

```
<Label>
    <Label.FontAttributes>
        Bold
    </Label.FontAttributes>
</Label>
```

Ou:

```
<Button>
    <Button.Margin>
        10
    </Button.Margin>
</Button>
```

---

# 7.3 Propriedades anexadas

O MAUI também possui **Attached Properties**, utilizadas para fornecer informações a partir de um objeto para outro.

Exemplo comum:

```
<Grid>
    <Label
        Grid.Row="0"
        Grid.Column="1"
        Text="Nome" />
</Grid>
```

Aqui:

```
Grid.Row="0"
Grid.Column="1"
```

são propriedades relacionadas ao `Grid`.

Elas informam ao `Grid` onde o elemento filho deve ser colocado.

---

# 8. `StaticResource`

`StaticResource` permite buscar um recurso definido anteriormente em um dicionário de recursos.

Imagine:

```
<ContentPage.Resources>
    <ResourceDictionary>

        <Color x:Key="PrimaryColor">
            #512BD4
        </Color>

    </ResourceDictionary>
</ContentPage.Resources>
```

Agora podemos utilizar:

```
<Button
    Text="Entrar"
    BackgroundColor="{StaticResource PrimaryColor}" />
```

A expressão:

```
{StaticResource PrimaryColor}
```

significa:

> Procure o recurso chamado `PrimaryColor`.

---

## 8.1 Por que utilizar recursos?

Sem recurso:

```
<Button BackgroundColor="#512BD4" />
<Button BackgroundColor="#512BD4" />
<Button BackgroundColor="#512BD4" />
<Button BackgroundColor="#512BD4" />
```

Com recurso:

```
<Button BackgroundColor="{StaticResource PrimaryColor}" />
<Button BackgroundColor="{StaticResource PrimaryColor}" />
<Button BackgroundColor="{StaticResource PrimaryColor}" />
<Button BackgroundColor="{StaticResource PrimaryColor}" />
```

Se a cor mudar:

```
<Color x:Key="PrimaryColor">
    #FF0000
</Color>
```

todos os controles que utilizam o recurso passam a utilizar a nova definição.

---

# 9. `DynamicResource`

`DynamicResource` também referencia um recurso, mas foi projetado para que o valor possa ser **atualizado dinamicamente quando o recurso muda**.

Exemplo:

```
<ContentPage.Resources>
    <ResourceDictionary>

        <Color x:Key="PageBackground">
            White
        </Color>

    </ResourceDictionary>
</ContentPage.Resources>
```

Uso:

```
<ContentPage
    BackgroundColor="{DynamicResource PageBackground}">
```

Se o recurso for alterado durante a execução:

```
Resources["PageBackground"] = Colors.Black;
```

elementos que utilizam `DynamicResource` podem refletir a mudança.

---

# `StaticResource` × `DynamicResource`

Essa diferença é muito importante.

|Característica|`StaticResource`|`DynamicResource`|
|---|---|---|
|Busca recurso|Sim|Sim|
|Valor pode ser atualizado em runtime|Não é seu objetivo|Sim|
|Atualização dinâmica|❌|✅|
|Ideal para recursos estáveis|✅|—|
|Ideal para temas/valores mutáveis|—|✅|
|Sintaxe|`{StaticResource Nome}`|`{DynamicResource Nome}`|

### Regra mental

```
StaticResource
      ↓
recurso estável

DynamicResource
      ↓
recurso que pode mudar durante a execução
```

---

# 10. Styles

`Style` permite definir um conjunto de propriedades que pode ser reutilizado.

Imagine vários botões:

```
<Button
    Text="Salvar"
    BackgroundColor="Blue"
    TextColor="White"
    FontSize="18" />

<Button
    Text="Enviar"
    BackgroundColor="Blue"
    TextColor="White"
    FontSize="18" />

<Button
    Text="Entrar"
    BackgroundColor="Blue"
    TextColor="White"
    FontSize="18" />
```

Existe muita repetição.

Podemos criar um `Style`.

```
<ContentPage.Resources>

    <Style x:Key="PrimaryButtonStyle"
           TargetType="Button">

        <Setter Property="BackgroundColor"
                Value="Blue" />

        <Setter Property="TextColor"
                Value="White" />

        <Setter Property="FontSize"
                Value="18" />

    </Style>

</ContentPage.Resources>
```

Agora:

```
<Button
    Text="Salvar"
    Style="{StaticResource PrimaryButtonStyle}" />

<Button
    Text="Enviar"
    Style="{StaticResource PrimaryButtonStyle}" />

<Button
    Text="Entrar"
    Style="{StaticResource PrimaryButtonStyle}" />
```

---

# 10.1 `Setter`

O `Setter` define uma propriedade que será aplicada pelo estilo.

```
<Setter
    Property="FontSize"
    Value="20" />
```

Estrutura:

```
Style
 ├── Setter
 │    ├── Property
 │    └── Value
 ├── Setter
 │    ├── Property
 │    └── Value
```

---

# 10.2 `TargetType`

Indica para qual tipo de controle o estilo foi criado.

```
<Style
    x:Key="PrimaryButtonStyle"
    TargetType="Button">
```

Nesse caso:

```
TargetType = Button
```

O estilo foi criado para `Button`.

---

# 10.3 Style implícito

Nem todo estilo precisa possuir `x:Key`.

Exemplo:

```
<Style TargetType="Label">

    <Setter
        Property="FontSize"
        Value="20" />

    <Setter
        Property="TextColor"
        Value="Blue" />

</Style>
```

Esse estilo é **implícito**.

Ele será aplicado automaticamente aos `Label` compatíveis dentro do escopo dos recursos.

```
<Label Text="Nome" />
<Label Text="Email" />
<Label Text="Telefone" />
```

Todos receberão o estilo.

---

## Style explícito × implícito

|Tipo|Possui `x:Key`?|Aplicação|
|---|---|---|
|Explícito|✅|Manual|
|Implícito|❌|Automática para o `TargetType`|

### Explícito

```
<Style
    x:Key="TituloStyle"
    TargetType="Label">
```

Uso:

```
<Label
    Text="Título"
    Style="{StaticResource TituloStyle}" />
```

### Implícito

```
<Style TargetType="Label">
```

Uso:

```
<Label Text="Título" />
```

---

# 11. Resources

`Resources` são recursos reutilizáveis disponíveis para os elementos XAML.

Podemos armazenar:

- cores;
- estilos;
- brushes;
- strings;
- objetos;
- templates;
- outros recursos.

---

## 11.1 Page Resources

Podemos definir recursos dentro de uma página:

```
<ContentPage.Resources>

    <ResourceDictionary>

        <Color x:Key="PrimaryColor">
            #512BD4
        </Color>

    </ResourceDictionary>

</ContentPage.Resources>
```

Depois:

```
<Label
    Text="Olá"
    TextColor="{StaticResource PrimaryColor}" />
```

---

# 11.2 Application Resources

Também podemos definir recursos globalmente no aplicativo.

Normalmente isso é feito em:

```
App.xaml
```

Exemplo:

```
<Application
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuApp.App">

    <Application.Resources>

        <ResourceDictionary>

            <Color x:Key="PrimaryColor">
                #512BD4
            </Color>

            <Color x:Key="SecondaryColor">
                #DFD8F7
            </Color>

        </ResourceDictionary>

    </Application.Resources>

</Application>
```

Agora diferentes páginas podem utilizar:

```
<Label
    TextColor="{StaticResource PrimaryColor}" />
```

---

# 11.3 Escopo dos Resources

Os recursos possuem **escopo**.

Uma visão simplificada:

```
Application
    │
    ├── Recursos globais
    │
    ├── Page A
    │     └── Recursos locais
    │
    └── Page B
          └── Recursos locais
```

Um recurso definido no `App.xaml` pode ser utilizado pelas páginas do aplicativo.

Um recurso definido dentro de uma página possui escopo mais restrito.

---

# 11.4 Exemplo completo

### App.xaml

```
<Application
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuApp.App">

    <Application.Resources>

        <ResourceDictionary>

            <Color x:Key="PrimaryColor">
                #512BD4
            </Color>

            <Style
                x:Key="PrimaryButtonStyle"
                TargetType="Button">

                <Setter
                    Property="BackgroundColor"
                    Value="{StaticResource PrimaryColor}" />

                <Setter
                    Property="TextColor"
                    Value="White" />

                <Setter
                    Property="FontSize"
                    Value="18" />

            </Style>

        </ResourceDictionary>

    </Application.Resources>

</Application>
```

### MainPage.xaml

```
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuApp.MainPage">

    <VerticalStackLayout Padding="20">

        <Label
            Text="Meu aplicativo"
            TextColor="{StaticResource PrimaryColor}"
            FontSize="28" />

        <Button
            Text="Entrar"
            Style="{StaticResource PrimaryButtonStyle}" />

        <Button
            Text="Cadastrar"
            Style="{StaticResource PrimaryButtonStyle}" />

    </VerticalStackLayout>

</ContentPage>
```

Temos aqui vários conceitos trabalhando juntos:

```
App.xaml
│
├── Color
│    └── PrimaryColor
│
└── Style
     └── PrimaryButtonStyle
          ├── BackgroundColor
          ├── TextColor
          └── FontSize
                  ↓
             MainPage.xaml
                  ↓
             Buttons
```

---

# 12. Diferenças importantes

## 12.1 XAML × C#

|XAML|C#|
|---|---|
|Interface declarativa|Lógica de programação|
|Elementos visuais|Objetos e métodos|
|Propriedades|Atribuições|
|Eventos declarados|Métodos manipuladores|
|Resources|Objetos reutilizáveis|
|Styles|Configuração reutilizável|

---

## 12.2 Elemento × atributo

```
<Label Text="Olá" />
```

|Parte|Significado|
|---|---|
|`Label`|Elemento|
|`Text`|Atributo/propriedade|
|`"Olá"`|Valor|

---

## 12.3 Propriedade × evento

```
<Button
    Text="Enviar"
    Clicked="Enviar_Clicked" />
```

|`Text`|`Clicked`|
|---|---|
|Propriedade|Evento|
|Configura o controle|Reage à interação|
|`"Enviar"`|`Enviar_Clicked`|

---

## 12.4 `x:Name` × `x:Key`

Essa diferença costuma gerar confusão.

### `x:Name`

Identifica um elemento visual:

```
<Label
    x:Name="lblNome"
    Text="Fernando" />
```

Pode ser acessado no Code-Behind:

```
lblNome.Text = "Novo nome";
```

### `x:Key`

Identifica um recurso:

```
<Color x:Key="PrimaryColor">
    Blue
</Color>
```

Pode ser recuperado:

```
{StaticResource PrimaryColor}
```

||`x:Name`|`x:Key`|
|---|---|---|
|Identifica|Elemento|Recurso|
|Uso principal|Code-Behind|Resource Dictionary|
|Exemplo|`x:Name="lbl"`|`x:Key="PrimaryColor"`|

---

# 13. Quadro de revisão

## 🧠 Resumo geral

|Conceito|O que faz|Exemplo|
|---|---|---|
|XAML|Declara a interface|`<Label Text="Olá" />`|
|Elemento|Representa um objeto|`<Button />`|
|Atributo|Configura uma propriedade|`Text="OK"`|
|`x:Name`|Nomeia elemento|`x:Name="btnSalvar"`|
|Namespace|Identifica tipos/recursos|`xmlns:x="..."`|
|Evento|Reage a ações|`Clicked="..."`|
|Propriedade|Configura estado|`Text="Olá"`|
|`StaticResource`|Obtém recurso|`{StaticResource Cor}`|
|`DynamicResource`|Obtém recurso atualizável|`{DynamicResource Cor}`|
|`Style`|Agrupa configurações|`<Style ...>`|
|`Setter`|Define propriedade no Style|`<Setter ...>`|
|`TargetType`|Define alvo do Style|`TargetType="Button"`|
|`Resources`|Armazena recursos reutilizáveis|`<Page.Resources>`|
|`x:Key`|Identifica recurso|`x:Key="PrimaryColor"`|

---

# 🎯 Exemplo para memorizar tudo

Este exemplo reúne praticamente todo o conteúdo:

```
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MeuApp.MainPage">

    <ContentPage.Resources>

        <ResourceDictionary>

            <Color x:Key="PrimaryColor">
                #512BD4
            </Color>

            <Style
                x:Key="ButtonStyle"
                TargetType="Button">

                <Setter
                    Property="BackgroundColor"
                    Value="{StaticResource PrimaryColor}" />

                <Setter
                    Property="TextColor"
                    Value="White" />

            </Style>

        </ResourceDictionary>

    </ContentPage.Resources>

    <VerticalStackLayout Padding="20">

        <Label
            x:Name="lblTitulo"
            Text="Meu aplicativo"
            FontSize="28"
            TextColor="{StaticResource PrimaryColor}" />

        <Entry
            x:Name="txtNome"
            Placeholder="Digite seu nome"
            TextChanged="Entry_TextChanged" />

        <Button
            x:Name="btnEnviar"
            Text="Enviar"
            Style="{StaticResource ButtonStyle}"
            Clicked="Button_Clicked" />

    </VerticalStackLayout>

</ContentPage>
```

E o Code-Behind:

```
namespace MeuApp;

public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
    }

    private void Entry_TextChanged(object sender, TextChangedEventArgs e)
    {
        lblTitulo.Text = e.NewTextValue;
    }

    private async void Button_Clicked(object sender, EventArgs e)
    {
        await DisplayAlertAsync(
            "Mensagem",
            $"Olá, {txtNome.Text}!",
            "OK");
    }
}
```

### O que está acontecendo?

```
ContentPage
│
├── xmlns
│     └── Namespaces
│
├── x:Class
│     └── associa XAML ao Code-Behind
│
├── Resources
│     ├── Color
│     │    └── x:Key
│     │
│     └── Style
│          ├── TargetType
│          └── Setters
│
└── VerticalStackLayout
      │
      ├── Label
      │    ├── x:Name
      │    ├── Properties
      │    └── StaticResource
      │
      ├── Entry
      │    ├── x:Name
      │    ├── Properties
      │    └── Event
      │
      └── Button
           ├── x:Name
           ├── Style
           └── Event
```

---

## 📝 O que mais cai em questões

Se o objetivo é **estudar .NET MAUI para prova/concurso**, memorize principalmente estas relações:

> **XAML → declaração da interface**

> **Elemento → objeto/controle**

> **Atributo → configuração de propriedade**

> **Propriedade → estado/configuração do objeto**

> **Evento → reação a uma ação**

> **`x:Name` → identifica elemento para referência**

> **`x:Key` → identifica recurso**

> **`Resources` → armazenamento de recursos reutilizáveis**

> **`Style` → conjunto reutilizável de propriedades**

> **`Setter` → define propriedades de um Style**

> **`StaticResource` → referencia recurso**

> **`DynamicResource` → referencia recurso que pode ser atualizado dinamicamente**

> **`xmlns` → namespace**

> **`xmlns:x` → namespace das diretivas `x:` do XAML**

Essa distinção entre **propriedade, evento, recurso, `x:Name`, `x:Key`, `StaticResource` e `DynamicResource`** é especialmente importante para não confundir os conceitos em exercícios práticos e questões teóricas.