# Configuração e navegação com FlyoutPage no .NET MAUI

## 1. O que é o FlyoutPage?

O `FlyoutPage` é um tipo de página do .NET MAUI utilizado para criar uma interface com **menu lateral**.

Ele possui basicamente duas partes:

- **Flyout**: representa o menu lateral.
    
- **Detail**: representa o conteúdo principal exibido ao usuário.
    

Podemos visualizar a estrutura dessa forma:

```text
FlyoutPage
│
├── Flyout
│   └── Menu lateral
│
└── Detail
    └── Conteúdo principal
```

Por exemplo, podemos ter:

```text
+------------------+--------------------------+
| Página 1          |                          |
| Página 2          |      Conteúdo           |
| Página 3          |      principal          |
|                  |                          |
+------------------+--------------------------+
       Flyout                 Detail
```

O menu lateral fica responsável pelas opções de navegação, enquanto o `Detail` apresenta a página selecionada.

---

# 2. Comportamento do Flyout em diferentes dispositivos

Uma das características importantes do `FlyoutPage` é que seu comportamento pode variar dependendo do tamanho e da orientação da tela.

Em um celular, normalmente não existe espaço suficiente para manter o menu lateral permanentemente aberto.

Por isso, o comportamento mais comum é:

```text
Celular

[☰] Conteúdo
```

Ao clicar no botão de menu:

```text
[Menu] | Conteúdo
```

Já em uma tela maior, como um computador ou tablet, podemos escolher diferentes comportamentos.

---

# 3. Propriedade FlyoutLayoutBehavior

Para controlar como o menu lateral deve se comportar, podemos utilizar a propriedade:

```csharp
FlyoutLayoutBehavior
```

Essa propriedade determina como o `Flyout` será apresentado em dispositivos com telas maiores.

Exemplo:

```xml
FlyoutLayoutBehavior="Popover"
```

ou:

```xml
FlyoutLayoutBehavior="Split"
```

---

# 4. Split

O comportamento `Split` mantém o menu lateral e o conteúdo principal visíveis ao mesmo tempo.

Visualmente:

```text
+------------------+--------------------------+
| Página 1          |                          |
| Página 2          |      Conteúdo           |
| Página 3          |      principal          |
|                  |                          |
+------------------+--------------------------+
```

Nesse comportamento, o menu não fica simplesmente escondido atrás do conteúdo.

Ele permanece dividido com o `Detail`.

Exemplo:

```xml
<FlyoutPage
    FlyoutLayoutBehavior="Split">
```

Esse comportamento é bastante adequado para telas maiores.

---

# 5. Popover

O comportamento `Popover` permite que o menu fique recolhido e seja aberto quando o usuário clicar no ícone do menu.

Exemplo:

```xml
<FlyoutPage
    FlyoutLayoutBehavior="Popover">
```

Quando recolhido:

```text
+--------------------------------------+
| ☰       Conteúdo principal           |
|                                      |
|                                      |
+--------------------------------------+
```

Quando o usuário clica no menu:

```text
+------------------+-------------------+
| Página 1         |                   |
| Página 2         |   Conteúdo        |
| Página 3         |                   |
|                  |                   |
+------------------+-------------------+
```

Nesse caso, o menu aparece sobre o conteúdo.

Ao clicar novamente ou selecionar o conteúdo, o menu pode voltar a ficar recolhido.

---

# 6. Outras opções de FlyoutLayoutBehavior

A aula também apresenta comportamentos específicos relacionados à orientação da tela.

As principais opções são:

|Opção|Comportamento|
|---|---|
|`Default`|Utiliza o comportamento padrão da plataforma|
|`Popover`|O menu pode ficar recolhido e aparecer sobre o conteúdo|
|`Split`|Menu e conteúdo ficam lado a lado|
|`SplitOnPortrait`|Utiliza o comportamento dividido quando a tela está na vertical|
|`SplitOnLandscape`|Utiliza o comportamento dividido quando a tela está na horizontal|

Essas opções são particularmente interessantes para tablets e computadores.

---

# 7. SplitOnPortrait

O `SplitOnPortrait` pode ser utilizado quando queremos que o menu fique dividido quando o dispositivo estiver na orientação vertical.

Exemplo:

```xml
<FlyoutPage
    FlyoutLayoutBehavior="SplitOnPortrait">
```

Isso pode ser interessante para dispositivos como tablets utilizados principalmente na vertical.

Exemplo:

```text
      Tablet na vertical

+------------------------+
| Menu    |   Conteúdo   |
|         |              |
| Página  |              |
| Página  |              |
+------------------------+
```

---

# 8. SplitOnLandscape

O `SplitOnLandscape` faz o contrário.

O comportamento dividido será utilizado quando o dispositivo estiver na orientação horizontal.

Exemplo:

```xml
<FlyoutPage
    FlyoutLayoutBehavior="SplitOnLandscape">
```

Esse comportamento pode ser interessante para tablets utilizados na horizontal.

Exemplo:

```text
Tablet na horizontal

+------------------+--------------------------+
| Menu             | Conteúdo                 |
|                  |                          |
| Página 1         |                          |
| Página 2         |                          |
| Página 3         |                          |
+------------------+--------------------------+
```

---

# 9. Comparação dos comportamentos

Podemos resumir dessa maneira:

|Comportamento|Menu|
|---|---|
|`Popover`|Recolhido, podendo aparecer sobre o conteúdo|
|`Split`|Sempre dividido com o conteúdo|
|`SplitOnPortrait`|Dividido quando estiver na vertical|
|`SplitOnLandscape`|Dividido quando estiver na horizontal|
|`Default`|Comportamento padrão definido pela plataforma|

---

# 10. Criando itens no menu

Depois de configurar o comportamento do menu, a aula passa para uma parte importante: fazer o menu realmente funcionar.

Para isso, foram criados alguns botões:

```xml
<Button Text="Página 1" />
<Button Text="Página 2" />
<Button Text="Página 3" />
```

Esses botões representam opções de navegação.

---

# 11. Alterando a aparência dos botões

Para deixar os botões mais parecidos com itens de menu, podemos remover o fundo.

Para isso, utilizamos:

```xml
BackgroundColor="Transparent"
```

Exemplo:

```xml
<Button
    Text="Página 1"
    BackgroundColor="Transparent" />
```

Também podemos definir a cor do texto:

```xml
TextColor="Black"
```

Então podemos ter:

```xml
<Button
    Text="Página 1"
    BackgroundColor="Transparent"
    TextColor="Black" />
```

O objetivo é fazer o botão parecer mais um item de menu do que um botão tradicional.

---

# 12. Evento Clicked

Cada botão precisa executar uma ação quando for clicado.

Para isso, utilizamos o evento:

```xml
Clicked
```

Exemplo:

```xml
<Button
    Text="Página 1"
    Clicked="OnButtonClickedPage1" />
```

Outro:

```xml
<Button
    Text="Página 2"
    Clicked="OnButtonClickedPage2" />
```

E:

```xml
<Button
    Text="Página 3"
    Clicked="OnButtonClickedPage3" />
```

Assim, cada botão possui seu próprio manipulador de evento.

---

# 13. O que acontece quando o botão é clicado?

A ideia principal da aula é:

> Quando o usuário clicar em uma opção do menu, devemos alterar o conteúdo apresentado na propriedade `Detail` do `FlyoutPage`.

Por exemplo:

```text
Página 1 → Detail = Página1
Página 2 → Detail = Página2
Página 3 → Detail = Página3
```

Dessa forma, o menu permanece sendo o mesmo, mas o conteúdo central muda.

---

# 14. A propriedade MainPage

Para acessar a página principal da aplicação, podemos utilizar:

```csharp
App.Current.MainPage
```

A propriedade `MainPage` representa a página principal da aplicação.

Porém, existe um detalhe importante.

A propriedade `MainPage` é uma referência do tipo `Page`.

Isso significa que ela pode representar diferentes tipos de páginas.

Por exemplo:

```text
Page
├── ContentPage
├── NavigationPage
├── FlyoutPage
├── TabbedPage
└── outros tipos
```

Por isso, se sabemos que nossa `MainPage` é especificamente um `FlyoutPage`, podemos fazer uma conversão.

---

# 15. Convertendo MainPage para FlyoutPage

Podemos fazer:

```csharp
var flyoutPage = App.Current.MainPage as FlyoutPage;
```

Agora temos uma referência que permite acessar as propriedades específicas do `FlyoutPage`.

Outra possibilidade seria utilizar conversão explícita:

```csharp
var flyoutPage = (FlyoutPage)App.Current.MainPage;
```

A diferença é que o `as` retorna `null` caso a conversão não seja possível, enquanto a conversão explícita pode gerar uma exceção.

---

# 16. A propriedade Detail

Depois de obter o `FlyoutPage`, podemos acessar:

```csharp
flyoutPage.Detail
```

A propriedade `Detail` representa a página que está sendo exibida como conteúdo principal.

Por exemplo:

```csharp
flyoutPage.Detail = new ContentPage();
```

Nesse caso, estamos substituindo o conteúdo principal por uma nova página.

---

# 17. Exemplo de navegação

Suponha que temos três páginas:

```csharp
Page1
Page2
Page3
```

No evento do botão Página 1:

```csharp
private void OnButtonClickedPage1(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new Page1();
}
```

No botão Página 2:

```csharp
private void OnButtonClickedPage2(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new Page2();
}
```

E no botão Página 3:

```csharp
private void OnButtonClickedPage3(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new Page3();
}
```

O algoritmo é basicamente o mesmo nos três casos.

A única coisa que muda é a página atribuída ao `Detail`.

---

# 18. Fluxo completo da navegação

O funcionamento pode ser representado assim:

```text
Usuário
   ↓
Clica em "Página 2"
   ↓
Evento Clicked
   ↓
Obtém App.Current.MainPage
   ↓
Converte para FlyoutPage
   ↓
Acessa a propriedade Detail
   ↓
Detail recebe Page2
   ↓
Página 2 aparece no conteúdo principal
```

---

# 19. Flyout e Detail

É importante compreender a diferença entre as duas propriedades.

### Flyout

Representa o menu lateral.

```csharp
flyoutPage.Flyout
```

É responsável pela parte de navegação/menu.

### Detail

Representa o conteúdo principal.

```csharp
flyoutPage.Detail
```

É a página que será apresentada para o usuário.

Podemos visualizar:

```text
              FlyoutPage
             /          \
            /            \
        Flyout          Detail
          ↓                ↓
      Menu lateral     Página atual
```

---

# 20. O menu também pode ser alterado

Um ponto importante mencionado na aula é que a programação não precisa necessariamente alterar apenas o `Detail`.

Como temos acesso ao `FlyoutPage`, podemos trabalhar com outras propriedades e comportamentos.

Por exemplo:

```csharp
flyoutPage.Detail
```

permite alterar o conteúdo.

Enquanto:

```csharp
flyoutPage.Flyout
```

permite trabalhar com o menu lateral.

Portanto, dependendo da necessidade da aplicação, podemos modificar diferentes partes da estrutura.

---

# 21. Exemplo completo

Um exemplo simplificado pode ficar assim.

## Menu

```xml
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml">

    <VerticalStackLayout>

        <Button
            Text="Página 1"
            BackgroundColor="Transparent"
            TextColor="Black"
            Clicked="OnButtonClickedPage1" />

        <Button
            Text="Página 2"
            BackgroundColor="Transparent"
            TextColor="Black"
            Clicked="OnButtonClickedPage2" />

        <Button
            Text="Página 3"
            BackgroundColor="Transparent"
            TextColor="Black"
            Clicked="OnButtonClickedPage3" />

    </VerticalStackLayout>

</ContentPage>
```

## Code-behind

```csharp
private void OnButtonClickedPage1(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new Page1();
}

private void OnButtonClickedPage2(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new Page2();
}

private void OnButtonClickedPage3(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new Page3();
}
```

---

# 22. Conceitos principais da aula

|Conceito|Explicação|
|---|---|
|`FlyoutPage`|Página que possui menu lateral e conteúdo principal|
|`Flyout`|Menu lateral|
|`Detail`|Conteúdo principal|
|`FlyoutLayoutBehavior`|Define o comportamento do menu em diferentes tamanhos/orientações|
|`Split`|Mantém menu e conteúdo lado a lado|
|`Popover`|Permite que o menu fique recolhido e apareça sobre o conteúdo|
|`SplitOnPortrait`|Divide o layout na orientação vertical|
|`SplitOnLandscape`|Divide o layout na orientação horizontal|
|`Clicked`|Evento executado quando um botão é clicado|
|`App.Current.MainPage`|Permite acessar a página principal da aplicação|
|`as FlyoutPage`|Faz uma conversão para `FlyoutPage`|
|`Detail`|Permite substituir a página apresentada no conteúdo principal|

---

# 23. O que foi aprendido

Nesta aula aprendemos que o `FlyoutPage` não serve apenas para criar um menu lateral. Ele também permite controlar como esse menu será apresentado de acordo com o dispositivo.

Em telas maiores, podemos utilizar comportamentos como:

```csharp
Split
Popover
SplitOnPortrait
SplitOnLandscape
```

Também aprendemos que podemos utilizar eventos de clique nos itens do menu para alterar o conteúdo principal da aplicação.

A lógica principal é:

```csharp
App.Current.MainPage
        ↓
FlyoutPage
        ↓
Detail
        ↓
Nova página
```

Assim, quando o usuário seleciona uma opção do menu, podemos substituir o conteúdo de `Detail` pela página correspondente.

Por exemplo:

```csharp
flyoutPage.Detail = new Page2();
```

Isso faz com que a `Page2` passe a ser apresentada como conteúdo principal.

O conceito mais importante desta aula é entender a relação:

```text
FlyoutPage
│
├── Flyout → Menu
│
└── Detail → Conteúdo
```

O `Flyout` permite ao usuário escolher uma opção e o `Detail` é atualizado para apresentar o conteúdo correspondente.