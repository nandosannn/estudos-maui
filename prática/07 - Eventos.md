
# Eventos e Gestos no .NET MAUI

# Índices

- [[#1. Eventos no XAML]]
    
- [[#2. Event Handlers]]
    
- [[#3. Clicked]]
    
- [[#4. TextChanged]]
    
- [[#5. CheckedChanged]]
    
- [[#6. SelectionChanged]]
    
- [[#7. Gestos]]
    
- [[#8. TapGestureRecognizer]]
    
- [[#9. SwipeGestureRecognizer]]
    
- [[#10. Eventos x Gestos]]
    
- [[#11. Tabela-resumo]]
    

---
# 1. Eventos no XAML

Eventos são mecanismos utilizados para fazer o aplicativo **reagir a alguma ação ou mudança**.

Por exemplo:

- usuário toca em um botão;
    
- usuário digita um texto;
    
- usuário marca um `CheckBox`;
    
- usuário seleciona um item;
    
- usuário toca em uma imagem;
    
- usuário desliza o dedo pela tela.
    

Podemos representar isso assim:

```text
Ação do usuário
      ↓
    Evento
      ↓
Event Handler
      ↓
Código C#
      ↓
Ação do aplicativo
```

## Exemplo

Um `Button` possui o evento `Clicked`.

```xml
<Button
    Text="Clique aqui"
    Clicked="Button_Clicked" />
```

Quando o usuário toca no botão:

```text
Usuário toca no botão
        ↓
Evento Clicked é disparado
        ↓
Button_Clicked() é executado
        ↓
Código C# é executado
```

---

## Eventos no XAML

No XAML, podemos associar um evento a um método utilizando:

```xml
Evento="NomeDoMetodo"
```

Exemplo:

```xml
<Button
    Text="Salvar"
    Clicked="Salvar_Clicked" />
```

O XAML informa:

> Quando o evento `Clicked` acontecer, execute o método `Salvar_Clicked`.

---

## Eventos x propriedades

É importante não confundir eventos com propriedades.

### Propriedade

Define uma característica ou estado do componente:

```xml
<Button
    Text="Salvar"
    IsEnabled="True" />
```

Aqui:

```text
Text       → propriedade
IsEnabled  → propriedade
```

### Evento

Representa algo que aconteceu:

```xml
<Button
    Clicked="Salvar_Clicked" />
```

Aqui:

```text
Clicked → evento
```

### Resumindo

```text
Propriedade → "como o componente está/configurado"

Evento      → "algo aconteceu"
```

---

# 2. Event Handlers

Um **Event Handler** é o método responsável por tratar um evento.

Por exemplo:

```xml
<Button
    Text="Clique"
    Clicked="Button_Clicked" />
```

No C#:

```csharp
private void Button_Clicked(
    object sender,
    EventArgs e)
{
    DisplayAlert(
        "Aviso",
        "Botão clicado!",
        "OK");
}
```

O método:

```csharp
Button_Clicked()
```

é o **event handler**.

---

## `sender`

O parâmetro `sender` representa o objeto que disparou o evento.

Exemplo:

```csharp
private void Button_Clicked(
    object sender,
    EventArgs e)
{
    Button button = (Button)sender;

    DisplayAlert(
        "Botão",
        button.Text,
        "OK");
}
```

Nesse caso, `sender` representa o `Button`.

Podemos pensar:

```text
sender
  ↓
Quem disparou o evento?
```

---

## `EventArgs`

O parâmetro `e` contém informações relacionadas ao evento.

```csharp
EventArgs e
```

Em eventos simples, pode não haver informações adicionais.

Porém, alguns eventos possuem tipos específicos de argumentos.

Por exemplo:

```csharp
TextChangedEventArgs
```

possui informações sobre a alteração do texto.

---

## Estrutura geral

Um Event Handler normalmente possui:

```csharp
private void NomeDoEvento(
    object sender,
    EventArgs e)
{
    // código executado quando o evento acontece
}
```

Alguns eventos utilizam um tipo específico:

```csharp
private void Entry_TextChanged(
    object sender,
    TextChangedEventArgs e)
{
}
```

---

# 3. Clicked

O evento `Clicked` é utilizado principalmente com `Button`.

Ele ocorre quando o usuário toca/clica no botão.

## XAML

```xml
<Button
    Text="Clique aqui"
    Clicked="Button_Clicked" />
```

## C#

```csharp
private async void Button_Clicked(
    object sender,
    EventArgs e)
{
    await DisplayAlert(
        "Mensagem",
        "Você clicou no botão!",
        "OK");
}
```

Fluxo:

```text
Usuário toca no Button
        ↓
Clicked
        ↓
Button_Clicked()
        ↓
Código executado
```

---

## Alterando um Label

XAML:

```xml
<VerticalStackLayout>

    <Label
        x:Name="lblMensagem"
        Text="Aguardando..." />

    <Button
        Text="Clique"
        Clicked="Button_Clicked" />

</VerticalStackLayout>
```

C#:

```csharp
private void Button_Clicked(
    object sender,
    EventArgs e)
{
    lblMensagem.Text = "Botão clicado!";
}
```

Resultado:

Antes:

```text
Aguardando...

[ Clique ]
```

Depois:

```text
Botão clicado!

[ Clique ]
```

---

# 4. TextChanged

O evento `TextChanged` ocorre quando o conteúdo de um campo de texto é alterado.

É muito utilizado com:

- `Entry`;
    
- `Editor`;
    
- validações;
    
- pesquisas;
    
- filtros;
    
- contadores de caracteres.
    

## Exemplo

```xml
<Entry
    Placeholder="Digite seu nome"
    TextChanged="Entry_TextChanged" />
```

C#:

```csharp
private void Entry_TextChanged(
    object sender,
    TextChangedEventArgs e)
{
    Console.WriteLine(e.NewTextValue);
}
```

---

## `OldTextValue`

Representa o texto anterior.

```csharp
e.OldTextValue
```

## `NewTextValue`

Representa o novo texto.

```csharp
e.NewTextValue
```

Podemos visualizar:

```text
Antes:

"João"

     ↓ usuário digita "S"

Depois:

"JoãoS"
```

Então:

```csharp
e.OldTextValue → "João"
e.NewTextValue → "JoãoS"
```

---

## Exemplo de contador

XAML:

```xml
<VerticalStackLayout>

    <Entry
        x:Name="entryNome"
        Placeholder="Digite algo"
        TextChanged="Entry_TextChanged" />

    <Label
        x:Name="lblContador"
        Text="0 caracteres" />

</VerticalStackLayout>
```

C#:

```csharp
private void Entry_TextChanged(
    object sender,
    TextChangedEventArgs e)
{
    int quantidade = e.NewTextValue?.Length ?? 0;

    lblContador.Text =
        $"{quantidade} caracteres";
}
```

Agora o contador é atualizado enquanto o usuário digita.

---

# 5. CheckedChanged

O evento `CheckedChanged` é utilizado quando o estado de um componente de seleção booleana muda.

Um exemplo clássico é o `CheckBox`.

## XAML

```xml
<CheckBox
    CheckedChanged="CheckBox_CheckedChanged" />
```

## C#

```csharp
private void CheckBox_CheckedChanged(
    object sender,
    CheckedChangedEventArgs e)
{
    if (e.Value)
    {
        DisplayAlert(
            "Aviso",
            "Marcado!",
            "OK");
    }
}
```

---

## `e.Value`

O `e.Value` indica o novo estado.

```text
true  → marcado
false → desmarcado
```

Exemplo:

```csharp
if (e.Value)
{
    // marcado
}
else
{
    // desmarcado
}
```

---

## Exemplo completo

```xml
<VerticalStackLayout>

    <CheckBox
        x:Name="checkAceite"
        CheckedChanged="CheckBox_CheckedChanged" />

    <Label
        x:Name="lblStatus"
        Text="Não aceito" />

</VerticalStackLayout>
```

C#:

```csharp
private void CheckBox_CheckedChanged(
    object sender,
    CheckedChangedEventArgs e)
{
    if (e.Value)
    {
        lblStatus.Text = "Aceito";
    }
    else
    {
        lblStatus.Text = "Não aceito";
    }
}
```

---

# 6. SelectionChanged

O evento `SelectionChanged` é utilizado quando a seleção de itens muda.

É especialmente importante em componentes como:

```text
CollectionView
```

Por exemplo:

```xml
<CollectionView
    ItemsSource="{Binding Pessoas}"
    SelectionMode="Single"
    SelectionChanged="CollectionView_SelectionChanged" />
```

---

## Event Handler

```csharp
private void CollectionView_SelectionChanged(
    object sender,
    SelectionChangedEventArgs e)
{
    var pessoa =
        e.CurrentSelection.FirstOrDefault()
        as Pessoa;

    if (pessoa != null)
    {
        DisplayAlert(
            "Selecionado",
            pessoa.Nome,
            "OK");
    }
}
```

---

## `CurrentSelection`

Representa os itens atualmente selecionados.

```csharp
e.CurrentSelection
```

Se o modo for:

```xml
SelectionMode="Single"
```

normalmente haverá um item.

Se for:

```xml
SelectionMode="Multiple"
```

poderá haver vários.

---

## `PreviousSelection`

Representa a seleção anterior:

```csharp
e.PreviousSelection
```

Assim:

```text
PreviousSelection
       ↓
seleção anterior

CurrentSelection
       ↓
seleção atual
```

---

## Fluxo

```text
Usuário toca em um item
          ↓
CollectionView detecta seleção
          ↓
SelectionChanged
          ↓
Event Handler
          ↓
CurrentSelection
          ↓
Código trata o item selecionado
```

---

# 7. Gestos

Eventos não são limitados a botões e controles tradicionais.

Em aplicações mobile, também podemos reagir a **gestos realizados pelo usuário**.

Exemplos:

```text
Toque
 ↓
TapGestureRecognizer

Deslize
 ↓
SwipeGestureRecognizer
```

Os gestos são adicionados utilizando **Gesture Recognizers**.

---

## Gesture Recognizer

Um `GestureRecognizer` detecta uma interação realizada pelo usuário.

Podemos pensar nele como:

```text
Gestura do usuário
        ↓
Recognizer detecta
        ↓
Evento
        ↓
Event Handler
        ↓
Código
```

---

# 8. TapGestureRecognizer

O `TapGestureRecognizer` detecta toques.

Pode ser usado em elementos como:

- `Label`;
    
- `Image`;
    
- `Border`;
    
- `Grid`;
    
- `VerticalStackLayout`;
    
- entre outros elementos visuais.
    

---

## Exemplo

```xml
<Label
    Text="Toque aqui">

    <Label.GestureRecognizers>

        <TapGestureRecognizer
            Tapped="Label_Tapped" />

    </Label.GestureRecognizers>

</Label>
```

C#:

```csharp
private async void Label_Tapped(
    object sender,
    TappedEventArgs e)
{
    await DisplayAlert(
        "Toque",
        "Você tocou no Label!",
        "OK");
}
```

---

## Por que usar TapGestureRecognizer?

Um `Button` já possui:

```xml
Clicked
```

Mas elementos como um `Label` ou `Image` não são tradicionalmente utilizados como botões.

O `TapGestureRecognizer` permite transformar a interação em algo clicável.

Por exemplo:

```text
┌──────────────────────┐
│      🖼️ IMAGEM       │
│                      │
│   toque para abrir   │
└──────────────────────┘
```

---

## Número de toques

O gesto também pode trabalhar com número de toques.

Exemplo:

```xml
<TapGestureRecognizer
    NumberOfTapsRequired="2"
    Tapped="Imagem_Tapped" />
```

Nesse caso:

```text
1 toque  → não executa
2 toques → executa
```

Isso permite implementar interações como **duplo toque**.

---

# 9. SwipeGestureRecognizer

O `SwipeGestureRecognizer` detecta gestos de deslize.

Por exemplo:

```text
← deslizar para esquerda

→ deslizar para direita

↑ deslizar para cima

↓ deslizar para baixo
```

---

## Exemplo

```xml
<Border>

    <Border.GestureRecognizers>

        <SwipeGestureRecognizer
            Direction="Left"
            Swiped="Border_Swiped" />

    </Border.GestureRecognizers>

</Border>
```

C#:

```csharp
private void Border_Swiped(
    object sender,
    SwipedEventArgs e)
{
    DisplayAlert(
        "Swipe",
        "Deslizou para a esquerda!",
        "OK");
}
```

---

## Direction

Podemos especificar a direção:

```xml
Direction="Left"
```

```xml
Direction="Right"
```

```xml
Direction="Up"
```

```xml
Direction="Down"
```

---

## Exemplo

```xml
<Image
    Source="imagem.png">

    <Image.GestureRecognizers>

        <SwipeGestureRecognizer
            Direction="Right"
            Swiped="Image_Swiped" />

    </Image.GestureRecognizers>

</Image>
```

Agora o aplicativo reage quando o usuário desliza a imagem para a direita.

---

# 10. Eventos x Gestos

É importante diferenciar os dois conceitos.

## Evento tradicional

Normalmente está associado a um controle e a uma ação específica.

Exemplo:

```xml
<Button
    Clicked="Button_Clicked" />
```

```text
Button
  ↓
Clicked
```

---

## Gesto

É uma interação física realizada pelo usuário.

Exemplo:

```xml
<TapGestureRecognizer
    Tapped="Label_Tapped" />
```

```text
Toque
 ↓
TapGestureRecognizer
 ↓
Tapped
```

---

## `SwipeView` x `SwipeGestureRecognizer`

Esses dois conceitos podem causar confusão.

### `SwipeGestureRecognizer`

Detecta o gesto de deslizar.

```text
Usuário desliza
      ↓
SwipeGestureRecognizer
      ↓
Swiped
      ↓
Código
```

É utilizado para **detectar o gesto**.

### `SwipeView`

É um controle específico que revela ações quando o usuário desliza.

```text
┌──────────────────────────┐
│ João Silva               │
└──────────────────────────┘

        deslizar →

┌──────────────────┬───────┐
│ João Silva       │Excluir│
└──────────────────┴───────┘
```

Portanto:

|Recurso|Finalidade|
|---|---|
|`SwipeGestureRecognizer`|Detectar um gesto de deslize|
|`SwipeView`|Criar uma interface de ações reveladas por deslize|

---

# 11. Tabela-resumo

|Conceito|O que faz|Exemplo|
|---|---|---|
|**Evento**|Indica que algo aconteceu|`Clicked`|
|**Event Handler**|Método que trata o evento|`Button_Clicked()`|
|`sender`|Objeto que disparou o evento|`Button`|
|`EventArgs`|Informações do evento|`EventArgs e`|
|`Clicked`|Detecta clique/toque em botão|`Button`|
|`TextChanged`|Detecta alteração de texto|`Entry`|
|`OldTextValue`|Texto anterior|`"João"`|
|`NewTextValue`|Novo texto|`"João Silva"`|
|`CheckedChanged`|Detecta mudança de estado|`CheckBox`|
|`e.Value`|Novo estado do controle|`true/false`|
|`SelectionChanged`|Detecta mudança de seleção|`CollectionView`|
|`CurrentSelection`|Seleção atual|Item selecionado|
|`PreviousSelection`|Seleção anterior|Item anteriormente selecionado|
|**Gestos**|Interações físicas do usuário|Toque/deslize|
|`GestureRecognizer`|Detecta um gesto|Base dos recognizers|
|`TapGestureRecognizer`|Detecta toque|`Tapped`|
|`NumberOfTapsRequired`|Define quantidade de toques|`2`|
|`SwipeGestureRecognizer`|Detecta deslize|`Swiped`|
|`Direction`|Define direção do swipe|`Left`, `Right`, `Up`, `Down`|
|`SwipeView`|Revela ações ao deslizar|Editar/Excluir|

---

# 12. Quadro mental para memorizar

```text
                    EVENTOS
                       │
          ┌────────────┴────────────┐
          │                         │
     CONTROLES                    GESTOS
          │                         │
     ┌────┼────┬────┐          ┌───┴────┐
     │    │    │    │          │        │
 Clicked Text Checked Selection  Tap     Swipe
     │    │    │      │         │        │
   Button Entry CheckBox CollectionView  │
                                         │
                              SwipeGestureRecognizer
```

---

# 13. Exemplos para memorizar

### Botão

```xml
<Button
    Text="Salvar"
    Clicked="Salvar_Clicked" />
```

```csharp
private void Salvar_Clicked(
    object sender,
    EventArgs e)
{
    // ação
}
```

### Entrada de texto

```xml
<Entry
    TextChanged="Entry_TextChanged" />
```

```csharp
private void Entry_TextChanged(
    object sender,
    TextChangedEventArgs e)
{
    // texto mudou
}
```

### CheckBox

```xml
<CheckBox
    CheckedChanged="CheckBox_CheckedChanged" />
```

```csharp
private void CheckBox_CheckedChanged(
    object sender,
    CheckedChangedEventArgs e)
{
    // estado mudou
}
```

### CollectionView

```xml
<CollectionView
    SelectionChanged="CollectionView_SelectionChanged" />
```

```csharp
private void CollectionView_SelectionChanged(
    object sender,
    SelectionChangedEventArgs e)
{
    // seleção mudou
}
```

### Toque

```xml
<TapGestureRecognizer
    Tapped="Elemento_Tapped" />
```

```csharp
private void Elemento_Tapped(
    object sender,
    TappedEventArgs e)
{
    // elemento tocado
}
```

### Deslize

```xml
<SwipeGestureRecognizer
    Direction="Left"
    Swiped="Elemento_Swiped" />
```

```csharp
private void Elemento_Swiped(
    object sender,
    SwipedEventArgs e)
{
    // elemento deslizado
}
```

---

# 14. Fluxo geral dos eventos

A ideia mais importante desta aula pode ser resumida em:

```text
┌───────────────────────┐
│   Usuário interage    │
└───────────┬───────────┘
            ↓
┌───────────────────────┐
│       Evento          │
│ Clicked / TextChanged │
│ CheckedChanged / etc. │
└───────────┬───────────┘
            ↓
┌───────────────────────┐
│    Event Handler      │
│    Método em C#       │
└───────────┬───────────┘
            ↓
┌───────────────────────┐
│   Lógica da aplicação │
└───────────────────────┘
```

Para gestos:

```text
Usuário faz gesto
       ↓
Gesture Recognizer
       ↓
Evento do gesto
       ↓
Event Handler
       ↓
Código C#
```

---

# 15. O que memorizar para concursos e prática

|Conceito|Palavra-chave para lembrar|
|---|---|
|Evento|Algo aconteceu|
|Event Handler|Trata o evento|
|`sender`|Quem disparou|
|`EventArgs`|Dados do evento|
|`Clicked`|Botão clicado|
|`TextChanged`|Texto alterado|
|`CheckedChanged`|Estado marcado/desmarcado|
|`SelectionChanged`|Seleção alterada|
|`TapGestureRecognizer`|Detecta toque|
|`SwipeGestureRecognizer`|Detecta deslize|
|`Tapped`|Evento do toque|
|`Swiped`|Evento do deslize|
|`CurrentSelection`|Seleção atual|
|`PreviousSelection`|Seleção anterior|
|`NewTextValue`|Novo texto|
|`OldTextValue`|Texto anterior|
|`e.Value`|Novo estado booleano|
|`Direction`|Direção do swipe|
|`NumberOfTapsRequired`|Quantidade de toques|