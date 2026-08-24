# NavigationPage no .NET MAUI

## 1. O que é a NavigationPage?

No .NET MAUI, a `NavigationPage` é um recurso utilizado para **gerenciar a navegação entre diferentes páginas de conteúdo (`ContentPage`)**.

Enquanto uma `ContentPage` representa uma tela da aplicação, a `NavigationPage` funciona como um **mecanismo de navegação**, permitindo que o usuário saia de uma página e avance para outra.

Por exemplo:

```text
Página 1 → Página 2 → Página 3
```

A `NavigationPage` também fornece recursos visuais e funcionais, como:

- Barra de título da página;
    
- Botão de voltar;
    
- Navegação entre páginas;
    
- Histórico das páginas visitadas;
    
- Gerenciamento da pilha de navegação;
    
- Transições de tela específicas de cada plataforma.
    

Portanto, podemos pensar na `NavigationPage` como uma estrutura responsável por **organizar e controlar o fluxo de navegação da aplicação**.

---

# 2. ContentPage x NavigationPage

É importante diferenciar esses dois conceitos.

### ContentPage

A `ContentPage` representa efetivamente uma **tela da aplicação**.

Ela contém os elementos da interface, como:

- `Label`;
    
- `Button`;
    
- `Entry`;
    
- `Image`;
    
- `Grid`;
    
- `VerticalStackLayout`;
    
- entre outros.
    

Exemplo:

```xml
<ContentPage>
    <!-- Conteúdo da página -->
</ContentPage>
```

### NavigationPage

A `NavigationPage` não é simplesmente mais uma tela de conteúdo.

Ela funciona como um **container responsável por controlar a navegação entre páginas**.

Por exemplo:

```csharp
MainPage = new NavigationPage(new Page1());
```

Nesse caso:

- `Page1` é a primeira página apresentada;
    
- `NavigationPage` passa a controlar a navegação;
    
- a aplicação poderá navegar posteriormente para `Page2`, `Page3` etc.
    

---

# 3. A barra de título

Uma das características visuais da `NavigationPage` é a apresentação de uma **barra de navegação/título**.

Cada `ContentPage` possui a propriedade:

```xml
Title="Página 1"
```

Por exemplo:

```xml
<ContentPage
    ...
    Title="Página 1">
```

Quando a página está sendo utilizada dentro de uma `NavigationPage`, esse título pode ser apresentado na barra de navegação.

Isso significa que o `Title` pertence à `ContentPage`, mas sua apresentação visual depende do contexto de navegação e da plataforma.

Por exemplo:

```text
+--------------------------------+
| Página 1                       |
+--------------------------------+
|                                |
|       Conteúdo da página       |
|                                |
+--------------------------------+
```

Ao navegar para a segunda página:

```text
+--------------------------------+
| Página 2                       |
+--------------------------------+
|                                |
|       Conteúdo da página       |
|                                |
+--------------------------------+
```

O título também é atualizado.

---

# 4. O conceito mais importante: pilha de navegação

Um dos conceitos fundamentais para entender a `NavigationPage` é o conceito de **pilha (stack)**.

A navegação funciona como uma pilha de páginas.

Imagine que inicialmente temos:

```text
Página 1
```

A página 1 está no topo da pilha:

```text
┌───────────┐
│ Página 1  │
└───────────┘
```

Quando navegamos para a página 2, ela é adicionada à pilha:

```text
┌───────────┐
│ Página 2  │ ← página atual
├───────────┤
│ Página 1  │
└───────────┘
```

Quando navegamos para a página 3:

```text
┌───────────┐
│ Página 3  │ ← página atual
├───────────┤
│ Página 2  │
├───────────┤
│ Página 1  │
└───────────┘
```

A página que está no topo é a página atualmente apresentada ao usuário.

---

# 5. O que acontece quando navegamos?

Suponha que o usuário esteja na página 1 e clique em um botão para ir para a página 2.

A página 1 não é simplesmente substituída.

A página 2 é adicionada à pilha de navegação.

```text
Página 1
   ↓
Página 2
```

Internamente, podemos representar assim:

```text
[ Página 1, Página 2 ]
```

A página 2 passa a ser a página atual.

Se o usuário navegar novamente:

```text
[ Página 1, Página 2, Página 3 ]
```

A página 3 passa a ser a página atual.

Esse comportamento permite que o sistema saiba **qual página deve ser exibida quando o usuário voltar**.

---

# 6. Como funciona o botão Voltar?

Quando estamos na página 3 e pressionamos o botão de voltar, a página 3 é removida do topo da pilha.

Antes:

```text
┌───────────┐
│ Página 3  │ ← atual
├───────────┤
│ Página 2  │
├───────────┤
│ Página 1  │
└───────────┘
```

Depois do retorno:

```text
┌───────────┐
│ Página 2  │ ← atual
├───────────┤
│ Página 1  │
└───────────┘
```

A página 2 volta a ser apresentada.

Esse mecanismo é conhecido como **pop**.

De forma simplificada:

```text
Push → adiciona uma página à pilha
Pop  → remove a página do topo da pilha
```

Portanto:

```text
Página 1
   ↓ Push
Página 2
   ↓ Push
Página 3
   ↓ Pop
Página 2
```

---

# 7. Criando uma NavigationPage

Para utilizar uma `NavigationPage`, precisamos criar uma instância dela e informar qual será a primeira página.

Por exemplo:

```csharp
MainPage = new NavigationPage(new Page1());
```

Nesse código:

```csharp
new Page1()
```

cria uma instância da primeira página.

Essa página é então colocada dentro da:

```csharp
NavigationPage
```

Portanto, a estrutura inicial será:

```text
NavigationPage
      │
      └── Page1
```

A partir desse momento, a aplicação possui uma estrutura de navegação.

---

# 8. Criando várias ContentPages

Na aula foram criadas três páginas:

```text
Page1
Page2
Page3
```

Todas são `ContentPage`.

Por exemplo:

```csharp
public partial class Page1 : ContentPage
{
    public Page1()
    {
        InitializeComponent();
    }
}
```

O mesmo conceito é aplicado às outras páginas.

A diferença está no conteúdo apresentado em cada uma.

---

# 9. Utilizando a propriedade Title

Cada página pode possuir um título:

```xml
Title="Página 1"
```

Por exemplo:

```xml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppNavigationPage.Page1"
    Title="Página 1">
```

Na segunda página:

```xml
Title="Página 2"
```

E na terceira:

```xml
Title="Página 3"
```

Quando ocorre a navegação, o título apresentado na barra de navegação acompanha a página atual.

---

# 10. Criando o botão de navegação

Para navegar da página 1 para a página 2, podemos criar um botão.

Exemplo:

```xml
<Button
    Text="Prosseguir"
    HorizontalOptions="End"
    Clicked="Button_Clicked" />
```

Nesse exemplo:

### `Text`

Define o texto apresentado no botão:

```xml
Text="Prosseguir"
```

### `HorizontalOptions`

Define o posicionamento horizontal do botão:

```xml
HorizontalOptions="End"
```

O valor `End` faz com que o botão seja posicionado no final do espaço disponível.

### `Clicked`

Define o evento que será executado quando o usuário clicar no botão:

```xml
Clicked="Button_Clicked"
```

---

# 11. O evento Clicked

Quando configuramos:

```xml
Clicked="Button_Clicked"
```

precisamos ter um método correspondente no arquivo `.xaml.cs`.

Por exemplo:

```csharp
private async void Button_Clicked(object sender, EventArgs e)
{
    await Navigation.PushAsync(new Page2());
}
```

Esse método será executado quando o usuário clicar no botão.

---

# 12. O método PushAsync

O principal comando apresentado na aula para realizar a navegação foi:

```csharp
Navigation.PushAsync(...)
```

O `PushAsync` adiciona uma nova página à pilha de navegação.

Por exemplo:

```csharp
await Navigation.PushAsync(new Page2());
```

O que acontece?

Primeiro:

```text
Página 1
```

Depois do `PushAsync`:

```text
Página 1
Página 2 ← atual
```

A página 2 passa a ser exibida.

Se posteriormente fizermos:

```csharp
await Navigation.PushAsync(new Page3());
```

teremos:

```text
Página 1
Página 2
Página 3 ← atual
```

---

# 13. Por que utilizar `await`?

O método utilizado normalmente é:

```csharp
await Navigation.PushAsync(new Page2());
```

Isso acontece porque `PushAsync` é uma operação assíncrona.

O `await` permite aguardar a conclusão dessa operação sem bloquear desnecessariamente a interface da aplicação.

Por isso, o método do evento normalmente é declarado como:

```csharp
private async void Button_Clicked(object sender, EventArgs e)
```

Temos:

```text
async → permite utilizar await
await → aguarda uma operação assíncrona
```

---

# 14. Como funciona a navegação completa?

Podemos imaginar o seguinte fluxo:

### Estado inicial

```text
[ Página 1 ]
```

### Usuário clica em "Prosseguir"

```csharp
await Navigation.PushAsync(new Page2());
```

Agora:

```text
[ Página 1 ]
[ Página 2 ] ← atual
```

### Usuário navega para a página 3

```csharp
await Navigation.PushAsync(new Page3());
```

Agora:

```text
[ Página 1 ]
[ Página 2 ]
[ Página 3 ] ← atual
```

### Usuário clica em Voltar

A página 3 é removida:

```text
[ Página 1 ]
[ Página 2 ] ← atual
```

### Usuário clica em Voltar novamente

```text
[ Página 1 ] ← atual
```

Esse é o funcionamento básico da pilha de navegação.

---

# 15. A página anterior é destruída?

Esse ponto merece atenção.

Na explicação da aula, é apresentado que a página anterior continua fazendo parte da pilha enquanto uma nova página está sobre ela.

Por exemplo:

```text
Página 2
Página 1
```

A página 1 continua sendo a página anterior dentro da navegação.

Quando fazemos o retorno, a página que estava no topo é removida da pilha e a anterior volta a ser apresentada.

Portanto, não devemos pensar simplesmente em:

```text
Página 1 → destruída
Página 2 → criada
```

O modelo mental mais adequado é:

```text
Página 1
   ↓
Push
   ↓
Página 1 + Página 2
```

A `NavigationPage` mantém o histórico necessário para realizar a navegação de retorno.

---

# 16. Animações de navegação

Outro ponto interessante apresentado na aula é que a transição entre páginas pode variar de acordo com a plataforma.

O .NET MAUI é multiplataforma e utiliza os recursos e comportamentos apropriados de cada sistema operacional.

Assim, a transição visual pode ser diferente em:

- Windows;
    
- Android;
    
- iOS;
    
- macOS.
    

Por exemplo, em determinada plataforma, a página atual pode deslizar para um lado enquanto a nova página entra pelo outro.

O importante é entender que a lógica de navegação permanece a mesma, mesmo que a animação visual seja diferente.

---

# 17. Estrutura geral do exemplo

Podemos representar o projeto da aula da seguinte maneira:

```text
App
 │
 └── NavigationPage
       │
       └── Page1
            │
            └── Botão "Prosseguir"
                    │
                    ↓
                  Page2
                    │
                    ↓
                  Page3
```

E a pilha de navegação:

```text
┌─────────────┐
│   Page 3    │ ← página atual
├─────────────┤
│   Page 2    │
├─────────────┤
│   Page 1    │
└─────────────┘
```

---

# 18. Conceitos importantes para memorizar

### `ContentPage`

Representa uma tela da aplicação.

### `NavigationPage`

Gerencia a navegação entre páginas.

### `Title`

Define o título da página, que pode ser apresentado na barra de navegação.

### `Navigation`

Permite acessar o sistema de navegação da página.

### `PushAsync`

Adiciona uma nova página à pilha de navegação.

```csharp
await Navigation.PushAsync(new Page2());
```

### `PopAsync`

Remove a página atual da pilha e retorna para a anterior.

```csharp
await Navigation.PopAsync();
```

### Stack

É a estrutura utilizada para manter a sequência das páginas navegadas.

```text
Page1
Page2
Page3
```

A página no topo é a página atual.

---

# 19. Exemplo completo

## Page1.xaml

```xml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppNavigationPage.Page1"
    Title="Página 1">

    <VerticalStackLayout
        Padding="20">

        <Label
            Text="Bem-vindo à Página 1"
            FontSize="30" />

        <Button
            Text="Prosseguir"
            HorizontalOptions="End"
            Clicked="Button_Clicked" />

    </VerticalStackLayout>

</ContentPage>
```

## Page1.xaml.cs

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

## App.xaml.cs

A `NavigationPage` pode ser configurada como a página principal:

```csharp
public App()
{
    InitializeComponent();

    MainPage = new NavigationPage(new Page1());
}
```

Assim, a estrutura inicial será:

```text
NavigationPage
      │
      └── Page1
```

Quando o botão for pressionado:

```text
NavigationPage
      │
      ├── Page1
      │
      └── Page2 ← atual
```

---

# 20. Resumo da aula

A `NavigationPage` é um mecanismo do .NET MAUI utilizado para **gerenciar a navegação entre diferentes `ContentPage`**.

Seu funcionamento é baseado principalmente em uma **pilha de navegação**.

Quando uma nova página é aberta utilizando:

```csharp
await Navigation.PushAsync(new Page2());
```

ela é adicionada ao topo da pilha.

Por exemplo:

```text
Page1
Page2
Page3
```

A `Page3` é a página atual.

Quando o usuário volta, a página que está no topo é removida e a página anterior volta a ser exibida.

Além disso, a `NavigationPage` fornece recursos como:

- Barra de navegação;
    
- Título da página;
    
- Botão de voltar;
    
- Histórico de navegação;
    
- Transições entre páginas;
    
- Gerenciamento da pilha de páginas.
    

A ideia principal que deve ser memorizada é:

```text
ContentPage = representa uma tela

NavigationPage = gerencia a navegação entre telas

PushAsync = adiciona uma tela à pilha

PopAsync = remove a tela atual da pilha

Stack = histórico/estrutura das páginas navegadas
```

Portanto, podemos resumir o funcionamento da aula da seguinte forma:

```text
              NavigationPage
                    │
                    ▼
                 Page 1
                    │
               PushAsync
                    │
                    ▼
                 Page 2
                    │
               PushAsync
                    │
                    ▼
                 Page 3
                    │
                PopAsync
                    │
                    ▼
                 Page 2
```

Esse modelo de navegação é especialmente útil em aplicações que possuem **várias telas e precisam permitir que o usuário avance e retorne entre elas**.

# Tabela

| #   | Conteúdo                            | Explicação                                                                                     | Exemplo / Conceito-chave                            |
| --- | ----------------------------------- | ---------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| 1   | **NavigationPage**                  | Estrutura responsável por gerenciar a navegação entre páginas da aplicação.                    | `NavigationPage`                                    |
| 2   | **ContentPage**                     | Representa uma tela individual da aplicação.                                                   | `Page1`, `Page2`, `Page3`                           |
| 3   | **NavigationPage x ContentPage**    | A `ContentPage` representa a tela; a `NavigationPage` controla a navegação entre as telas.     | `NavigationPage(new Page1())`                       |
| 4   | **Barra de navegação**              | A `NavigationPage` fornece uma área superior que pode exibir o título e recursos de navegação. | Barra superior                                      |
| 5   | **Title**                           | Define o título associado à página, que pode ser exibido na barra de navegação.                | `Title="Página 1"`                                  |
| 6   | **Pilha de navegação (Stack)**      | As páginas são organizadas em uma pilha durante a navegação.                                   | `Page1 → Page2 → Page3`                             |
| 7   | **Página atual**                    | A página que está no topo da pilha é a página atualmente apresentada ao usuário.               | `Page3` é a atual                                   |
| 8   | **PushAsync**                       | Adiciona uma nova página ao topo da pilha de navegação.                                        | `await Navigation.PushAsync(new Page2());`          |
| 9   | **PopAsync**                        | Remove a página atual do topo da pilha e retorna para a página anterior.                       | `await Navigation.PopAsync();`                      |
| 10  | **Botão de navegação**              | Pode ser utilizado para iniciar a navegação para outra página.                                 | `Button`                                            |
| 11  | **Evento Clicked**                  | Executa um método quando o usuário clica no botão.                                             | `Clicked="Button_Clicked"`                          |
| 12  | **Code Behind**                     | Arquivo `.xaml.cs` onde podemos implementar a lógica dos eventos e da navegação.               | `Page1.xaml.cs`                                     |
| 13  | **async/await**                     | Utilizados porque os métodos de navegação são assíncronos.                                     | `async void` + `await`                              |
| 14  | **Histórico de navegação**          | A pilha mantém as páginas anteriores para possibilitar o retorno.                              | `Page1 → Page2 → Page3`                             |
| 15  | **Botão Voltar**                    | A `NavigationPage` pode fornecer o mecanismo de retorno entre páginas.                         | Voltar de `Page3` para `Page2`                      |
| 16  | **Transição de páginas**            | A animação da navegação pode variar de acordo com o sistema operacional.                       | Windows, Android, iOS etc.                          |
| 17  | **Instanciação da primeira página** | A primeira página é definida no momento da criação da `NavigationPage`.                        | `new NavigationPage(new Page1())`                   |
| 18  | **Navegação para outra página**     | A página atual permanece no histórico enquanto a nova página é adicionada à pilha.             | `Page1 + Page2`                                     |
| 19  | **Remoção da página atual**         | Ao voltar, a página do topo é retirada da pilha.                                               | `Page3 → PopAsync() → Page2`                        |
| 20  | **Fluxo completo**                  | A navegação segue o modelo de adicionar e remover páginas da pilha.                            | `Page1 → Push → Page2 → Push → Page3 → Pop → Page2` |

### Resumo para memorizar

|Conceito|Função|
|---|---|
|**ContentPage**|Representa uma tela|
|**NavigationPage**|Gerencia a navegação entre telas|
|**Title**|Define o título da página|
|**Navigation**|Dá acesso ao sistema de navegação|
|**PushAsync()**|Adiciona uma página à pilha|
|**PopAsync()**|Remove a página atual|
|**Stack**|Mantém o histórico das páginas|
|**Clicked**|Detecta o clique em um botão|
|**async/await**|Trabalha com a navegação assíncrona|

**Fluxo principal:**

```
Page 1
   │
   │ PushAsync()
   ▼
Page 2
   │
   │ PushAsync()
   ▼
Page 3
   │
   │ PopAsync()
   ▼
Page 2
```