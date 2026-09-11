
# Índice

- [[#1. CollectionView]]
- [[#2. ListView]]
- [[#3. CarouselView]]
- [[#4. Border]]
- [[#5. Frame]]
- [[#6. SwipeView]]
- [[#7. RefreshView]]
- [[#8. ActivityIndicator]]
- [[#9. ProgressBar]]
- [[#10. ActivityIndicator x ProgressBar]]
- [[#11. WebView]]
- [[#12. Como esses componentes se relacionam]]
- [[#13. Exemplo completo]]
- [[#14. Tabela-resumo geral]]
- [[#15. Diferenças que você precisa saber]]
- [[#16. O que estudar e praticar]]
# Controles e Interfaces no .NET MAUI

Depois dos componentes básicos (`Label`, `Button`, `Image`, `Entry`) e dos layouts, o próximo passo é entender os **controles usados para exibir coleções, organizar conteúdo visual, indicar estados de processamento e incorporar conteúdo externo**.

Os componentes desta etapa podem ser agrupados assim:

| Categoria                | Componentes                        |
| ------------------------ | ---------------------------------- |
| 📋 Listas e coleções     | `CollectionView`, `ListView`       |
| 🎠 Navegação visual      | `CarouselView`                     |
| 🧱 Containers visuais    | `Border`, `Frame`                  |
| 👆 Interação por gesto   | `SwipeView`                        |
| 🔄 Atualização           | `RefreshView`                      |
| ⏳ Progresso/carregamento | `ActivityIndicator`, `ProgressBar` |
| 🌐 Conteúdo web          | `WebView`                          |

---

# 1. `CollectionView`

O `CollectionView` é um dos componentes **mais importantes para trabalhar com listas no .NET MAUI**.

Ele serve para apresentar uma coleção de objetos de forma organizada.

Por exemplo:

```
┌──────────────────────────┐
│ João Silva               │
│ joao@email.com           │
├──────────────────────────┤
│ Maria Santos             │
│ maria@email.com          │
├──────────────────────────┤
│ Pedro Oliveira           │
│ pedro@email.com          │
└──────────────────────────┘
```

## Conceito

Imagine que você tenha:

```
List<string> nomes = new()
{
    "João",
    "Maria",
    "Pedro",
    "Ana"
};
```

Você pode utilizar o `CollectionView` para transformar essa coleção em elementos visuais.

### Exemplo simples

```
<CollectionView ItemsSource="{Binding Nomes}">
    <CollectionView.ItemTemplate>
        <DataTemplate>
            <Label
                Text="{Binding .}"
                FontSize="20"
                Padding="10" />
        </DataTemplate>
    </CollectionView.ItemTemplate>
</CollectionView>
```

O ponto mais importante é:

```
ItemsSource="{Binding Nomes}"
```

`ItemsSource` indica **de onde vêm os itens da lista**.

---

## `ItemTemplate`

O `ItemTemplate` define **como cada elemento da coleção será desenhado**.

```
<CollectionView.ItemTemplate>
    <DataTemplate>
        <Label Text="{Binding .}" />
    </DataTemplate>
</CollectionView.ItemTemplate>
```

Se a lista for:

```
João
Maria
Pedro
```

o template será aplicado individualmente:

```
Label → João
Label → Maria
Label → Pedro
```

---

## Trabalhando com objetos

É ainda mais comum utilizar objetos.

### Modelo

```
public class Pessoa
{
    public string Nome { get; set; }
    public int Idade { get; set; }
}
```

### Lista

```
public List<Pessoa> Pessoas { get; set; } = new()
{
    new Pessoa { Nome = "João", Idade = 25 },
    new Pessoa { Nome = "Maria", Idade = 30 },
    new Pessoa { Nome = "Pedro", Idade = 22 }
};
```

### XAML

```
<CollectionView ItemsSource="{Binding Pessoas}">
    <CollectionView.ItemTemplate>
        <DataTemplate>
            <VerticalStackLayout Padding="10">

                <Label
                    Text="{Binding Nome}"
                    FontSize="20" />

                <Label
                    Text="{Binding Idade}"
                    FontSize="14" />

            </VerticalStackLayout>
        </DataTemplate>
    </CollectionView.ItemTemplate>
</CollectionView>
```

Aqui:

```
Text="{Binding Nome}"
```

pega a propriedade `Nome` do objeto atual.

---

## Layout da CollectionView

Uma das grandes vantagens do `CollectionView` é poder alterar a organização dos itens.

### Lista vertical

```
<CollectionView ItemsLayout="VerticalList">
```

Resultado:

```
Item 1
Item 2
Item 3
Item 4
```

### Lista horizontal

```
<CollectionView ItemsLayout="HorizontalList">
```

Resultado:

```
Item 1 → Item 2 → Item 3 → Item 4
```

### Grid

```
<CollectionView>
    <CollectionView.ItemsLayout>
        <GridItemsLayout
            Orientation="Vertical"
            Span="2" />
    </CollectionView.ItemsLayout>
</CollectionView>
```

Resultado:

```
┌─────────┬─────────┐
│ Item 1  │ Item 2  │
├─────────┼─────────┤
│ Item 3  │ Item 4  │
├─────────┼─────────┤
│ Item 5  │ Item 6  │
└─────────┴─────────┘
```

`Span="2"` significa **duas colunas**.

---

## Seleção

Você pode permitir que o usuário selecione itens:

```
<CollectionView
    ItemsSource="{Binding Pessoas}"
    SelectionMode="Single"
    SelectionChanged="CollectionView_SelectionChanged">
```

No Code Behind:

```
private void CollectionView_SelectionChanged(
    object sender,
    SelectionChangedEventArgs e)
{
    var pessoa = e.CurrentSelection.FirstOrDefault()
        as Pessoa;

    if (pessoa != null)
    {
        DisplayAlert(
            "Pessoa",
            pessoa.Nome,
            "OK");
    }
}
```

### Modos

|`SelectionMode`|Comportamento|
|---|---|
|`None`|Não permite seleção|
|`Single`|Apenas um item|
|`Multiple`|Vários itens|

---

# 2. `ListView`

O `ListView` também serve para apresentar listas.

Exemplo:

```
<ListView ItemsSource="{Binding Nomes}">
    <ListView.ItemTemplate>
        <DataTemplate>
            <TextCell Text="{Binding .}" />
        </DataTemplate>
    </ListView.ItemTemplate>
</ListView>
```

Historicamente, o `ListView` foi bastante utilizado no Xamarin.Forms e versões anteriores do MAUI.

Porém, para novos projetos, **`CollectionView normalmente é a escolha preferida**.

---

## `ListView` x `CollectionView`

|Característica|`ListView`|`CollectionView`|
|---|---|---|
|Exibir listas|✅|✅|
|Grid|Limitado|✅|
|Lista horizontal|❌/limitado|✅|
|Seleção|✅|✅|
|Flexibilidade|Menor|Maior|
|Uso em projetos novos|Menos recomendado|**Preferível**|
|Performance/flexibilidade|Boa|Geralmente melhor|

### Regra prática

> **Para uma lista nova em .NET MAUI, pense primeiro em `CollectionView`.**

---

# 3. `CarouselView`

O `CarouselView` apresenta elementos como um **carrossel**, permitindo navegar horizontalmente entre eles.

Muito utilizado para:

- banners;
- produtos;
- imagens;
- onboarding;
- cards;
- destaques.

Exemplo:

```
<CarouselView ItemsSource="{Binding Produtos}">
    <CarouselView.ItemTemplate>
        <DataTemplate>

            <VerticalStackLayout
                Padding="20">

                <Image
                    Source="{Binding Imagem}"
                    HeightRequest="200" />

                <Label
                    Text="{Binding Nome}"
                    FontSize="24" />

                <Label
                    Text="{Binding Preco}"
                    FontSize="18" />

            </VerticalStackLayout>

        </DataTemplate>
    </CarouselView.ItemTemplate>
</CarouselView>
```

Visualmente:

```
        ← deslize →

┌─────────────────────┐
│                     │
│       PRODUTO       │
│                     │
│       R$ 99,90      │
│                     │
└─────────────────────┘

        ● ○ ○ ○
```

---

## `CarouselView` x `CollectionView`

|Componente|Principal finalidade|
|---|---|
|`CollectionView`|Mostrar vários itens em uma lista|
|`CarouselView`|Mostrar itens um de cada vez em sequência|

Exemplo:

**CollectionView:**

```
Produto A
Produto B
Produto C
Produto D
```

**CarouselView:**

```
← Produto A →
```

Depois:

```
← Produto B →
```

---

# 4. `Border`

O `Border` é um container utilizado para criar **bordas, fundos, cantos arredondados e elementos visuais personalizados**.

Ele é extremamente útil para criar cards.

```
<Border
    Stroke="Gray"
    StrokeThickness="2"
    Padding="15">

    <Label
        Text="Olá, mundo!"
        FontSize="20" />

</Border>
```

---

## Cantos arredondados

Você pode utilizar:

```
<Border
    Stroke="Gray"
    StrokeThickness="2"
    StrokeShape="RoundRectangle 15"
    Padding="15">
```

O `15` representa o arredondamento.

---

## Fundo

```
<Border
    BackgroundColor="LightBlue"
    Stroke="Blue"
    Padding="20">

    <Label
        Text="Card"
        FontSize="20" />

</Border>
```

---

## Exemplo de card

```
<Border
    Padding="20"
    Stroke="Gray"
    StrokeShape="RoundRectangle 15">

    <VerticalStackLayout Spacing="10">

        <Label
            Text="João Silva"
            FontSize="22"
            FontAttributes="Bold" />

        <Label
            Text="Desenvolvedor"
            FontSize="16" />

        <Button
            Text="Ver perfil" />

    </VerticalStackLayout>

</Border>
```

O `Border` pode conter praticamente qualquer outro elemento.

---

# 5. `Frame`

O `Frame` também foi muito utilizado para criar containers com aparência de card.

Exemplo:

```
<Frame
    Padding="20"
    CornerRadius="15"
    HasShadow="True">

    <Label
        Text="Meu Card"
        FontSize="20" />

</Frame>
```

Historicamente, o `Frame` era bastante utilizado para:

- bordas;
- cantos arredondados;
- sombras;
- cards.

Entretanto, no .NET MAUI moderno, o **`Border` é geralmente preferível** para esse tipo de composição visual.

---

## `Border` x `Frame`

|Característica|`Border`|`Frame`|
|---|---|---|
|Container|✅|✅|
|Bordas|✅|✅|
|Cantos arredondados|✅|✅|
|Personalização|⭐⭐⭐⭐⭐|⭐⭐⭐|
|Abordagem moderna|**Sim**|Mais legada|
|Cards|✅|✅|

### Regra prática

> Aprenda os dois, mas para novos componentes visuais, **prefira `Border`**.

---

# 6. `SwipeView`

O `SwipeView` permite executar ações quando o usuário **desliza um elemento para o lado**.

Muito comum em listas.

Por exemplo:

```
┌──────────────────────────────┐
│ João Silva              →    │
└──────────────────────────────┘
```

Ao deslizar:

```
┌─────────────────────┬─────────┬─────────┐
│ João Silva          │ Editar  │ Excluir │
└─────────────────────┴─────────┴─────────┘
```

---

## Exemplo

```
<SwipeView>

    <SwipeView.RightItems>

        <SwipeItems>

            <SwipeItem
                Text="Excluir"
                BackgroundColor="Red"
                Invoked="Excluir_Clicked" />

        </SwipeItems>

    </SwipeView.RightItems>

    <Grid Padding="20">

        <Label
            Text="João Silva"
            FontSize="20" />

    </Grid>

</SwipeView>
```

---

## Direções

Você pode ter ações:

```
<SwipeView.LeftItems>
```

ou:

```
<SwipeView.RightItems>
```

Também existem:

```
<SwipeView.TopItems>
```

e:

```
<SwipeView.BottomItems>
```

---

## Exemplo com editar e excluir

```
<SwipeView>

    <SwipeView.RightItems>

        <SwipeItems>

            <SwipeItem
                Text="Editar"
                Invoked="Editar_Clicked" />

            <SwipeItem
                Text="Excluir"
                Invoked="Excluir_Clicked" />

        </SwipeItems>

    </SwipeView.RightItems>

    <Label
        Text="João Silva"
        Padding="20" />

</SwipeView>
```

É especialmente útil dentro de `CollectionView`.

---

# 7. `RefreshView`

O `RefreshView` implementa o famoso **"puxar para atualizar"**.

Muito comum em aplicativos mobile:

```
        ↓ puxe

┌───────────────────────┐
│                       │
│      Carregando...    │
│                       │
│      Item 1           │
│      Item 2           │
│      Item 3           │
│                       │
└───────────────────────┘
```

---

## Exemplo

```
<RefreshView
    IsRefreshing="{Binding IsRefreshing}"
    Command="{Binding RefreshCommand}">

    <CollectionView
        ItemsSource="{Binding Pessoas}" />

</RefreshView>
```

O usuário desliza a lista para baixo e o comando é executado.

---

## Code Behind

Um exemplo simples:

```
<RefreshView
    x:Name="refreshView"
    Refreshing="RefreshView_Refreshing">

    <CollectionView
        ItemsSource="{Binding Pessoas}" />

</RefreshView>
```

C#:

```
private async void RefreshView_Refreshing(
    object sender,
    EventArgs e)
{
    await CarregarDados();

    refreshView.IsRefreshing = false;
}
```

---

## Fluxo

```
Usuário desliza para baixo
          ↓
RefreshView detecta gesto
          ↓
Executa atualização
          ↓
Busca dados
          ↓
Atualiza CollectionView
          ↓
Encerra indicador
```

---

# 8. `ActivityIndicator`

O `ActivityIndicator` mostra que uma operação está acontecendo.

Normalmente aparece como uma animação:

```
     ◌
   Carregando...
```

Exemplo:

```
<ActivityIndicator
    IsRunning="True"
    IsVisible="True" />
```

---

## `IsRunning`

Controla se a animação está executando.

```
IsRunning="True"
```

Executando.

```
IsRunning="False"
```

Parado.

---

## Exemplo prático

```
<VerticalStackLayout>

    <ActivityIndicator
        x:Name="loading"
        IsVisible="False"
        IsRunning="False" />

    <Button
        Text="Carregar"
        Clicked="Carregar_Clicked" />

</VerticalStackLayout>
```

C#:

```
private async void Carregar_Clicked(
    object sender,
    EventArgs e)
{
    loading.IsVisible = true;
    loading.IsRunning = true;

    await Task.Delay(3000);

    loading.IsRunning = false;
    loading.IsVisible = false;
}
```

### Quando utilizar?

Quando você **não sabe exatamente quanto tempo a operação vai durar**.

Exemplo:

```
Consultando API...
Login...
Carregando banco...
Processando dados...
```

---

# 9. `ProgressBar`

O `ProgressBar` também mostra progresso, mas existe uma diferença importante.

Ele mostra **quanto de uma operação já foi concluído**.

```
Download

████████████░░░░░░░░ 60%
```

Exemplo:

```
<ProgressBar
    Progress="0.6" />
```

O valor vai de:

```
0 ──────────────── 1
```

Onde:

|Valor|Progresso|
|---|---|
|`0`|0%|
|`0.25`|25%|
|`0.5`|50%|
|`0.75`|75%|
|`1`|100%|

---

## Exemplo

```
<ProgressBar
    x:Name="progressBar"
    Progress="0" />
```

C#:

```
progressBar.Progress = 0.5;
```

Resultado:

```
██████████░░░░░░░░░░ 50%
```

---

## Atualizando progressivamente

```
for (int i = 0; i <= 100; i++)
{
    progressBar.Progress = i / 100.0;

    await Task.Delay(50);
}
```

---

# 10. `ActivityIndicator` x `ProgressBar`

Essa diferença é **muito importante**.

|Característica|`ActivityIndicator`|`ProgressBar`|
|---|---|---|
|Indica carregamento|✅|✅|
|Mostra percentual|❌|✅|
|Sabe quando termina?|Não necessariamente|Geralmente sim|
|Progresso indeterminado|✅|❌|
|Download|Pode ser usado|**Ideal**|
|Consulta API|**Ideal**|Nem sempre|
|Animação de carregamento|✅|❌|

### Exemplo

Se você está esperando uma API:

```
🔄 Carregando...
```

Use:

```
<ActivityIndicator />
```

Se está baixando um arquivo de 100 MB:

```
████████████░░░░ 60%
```

Use:

```
<ProgressBar />
```

---

# 11. `WebView`

O `WebView` permite exibir **conteúdo web dentro do aplicativo**.

Por exemplo:

```
Aplicativo
┌─────────────────────────┐
│                         │
│       Página Web        │
│                         │
│   www.exemplo.com       │
│                         │
└─────────────────────────┘
```

Exemplo simples:

```
<WebView
    Source="https://www.google.com"
    HeightRequest="500" />
```

Ele abre a página dentro da aplicação.

---

## URL

```
<WebView
    Source="https://www.exemplo.com" />
```

---

## HTML diretamente

Você também pode fornecer HTML:

```
<WebView>

    <WebView.Source>

        <HtmlWebViewSource>
            <HtmlWebViewSource.Html>
                <![CDATA[
                    <html>
                        <body>
                            <h1>Olá!</h1>
                            <p>Conteúdo HTML.</p>
                        </body>
                    </html>
                ]]>
            </HtmlWebViewSource.Html>
        </HtmlWebViewSource>

    </WebView.Source>

</WebView>
```

---

## Casos de uso

`WebView` pode ser usado para:

- páginas web;
- documentação;
- conteúdo HTML;
- sistemas web;
- páginas de pagamento;
- termos de uso;
- conteúdos externos.

Mas é importante lembrar:

> `WebView` não transforma uma página web em uma aplicação MAUI nativa. Ele simplesmente incorpora um navegador dentro do aplicativo.

---

# 12. Como esses componentes se relacionam

Uma aplicação real pode combinar vários deles.

Por exemplo, imagine um aplicativo de produtos:

```
┌────────────────────────────────┐
│          Produtos              │
│                                │
│ ┌────────────────────────────┐ │
│ │        Produto 1           │ │
│ │        R$ 99,90            │ │
│ └────────────────────────────┘ │
│                                │
│ ┌────────────────────────────┐ │
│ │        Produto 2           │ │
│ │        R$ 49,90            │ │
│ └────────────────────────────┘ │
│                                │
│          ↓ puxar               │
│                                │
└────────────────────────────────┘
```

Poderíamos ter:

```
RefreshView
    │
    └── CollectionView
          │
          └── Border
                │
                ├── Image
                ├── Label
                └── Button
```

E dentro dos itens:

```
CollectionView
      │
      └── SwipeView
            ├── Editar
            └── Excluir
```

---

# 13. Exemplo completo

Imagine uma tela de produtos.

```
<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MinhaApp.MainPage">

    <RefreshView
        x:Name="refreshView"
        Refreshing="RefreshView_Refreshing">

        <CollectionView
            ItemsSource="{Binding Produtos}">

            <CollectionView.ItemTemplate>

                <DataTemplate>

                    <SwipeView>

                        <SwipeView.RightItems>

                            <SwipeItems>

                                <SwipeItem
                                    Text="Excluir"
                                    Invoked="Excluir_Clicked" />

                            </SwipeItems>

                        </SwipeView.RightItems>

                        <Border
                            Margin="10"
                            Padding="15"
                            Stroke="Gray"
                            StrokeShape="RoundRectangle 15">

                            <VerticalStackLayout
                                Spacing="10">

                                <Label
                                    Text="{Binding Nome}"
                                    FontSize="20"
                                    FontAttributes="Bold" />

                                <Label
                                    Text="{Binding Preco}"
                                    FontSize="16" />

                                <Button
                                    Text="Comprar" />

                            </VerticalStackLayout>

                        </Border>

                    </SwipeView>

                </DataTemplate>

            </CollectionView.ItemTemplate>

        </CollectionView>

    </RefreshView>

</ContentPage>
```

Observe quantos conceitos foram combinados:

```
RefreshView
     ↓
CollectionView
     ↓
ItemTemplate
     ↓
SwipeView
     ↓
Border
     ↓
VerticalStackLayout
     ↓
Label + Button
```

Essa combinação é extremamente comum em aplicações MAUI.

---

# 14. Tabela-resumo geral

|Componente|Para que serve|Exemplo de uso|
|---|---|---|
|`CollectionView`|Exibir coleções|Lista de usuários|
|`ListView`|Exibir listas|Listas legadas|
|`CarouselView`|Exibir itens em carrossel|Banners|
|`Border`|Criar containers visuais|Cards|
|`Frame`|Criar containers/cards|Interfaces antigas|
|`SwipeView`|Ações por deslize|Editar/excluir|
|`RefreshView`|Atualizar conteúdo por gesto|Atualizar lista|
|`ActivityIndicator`|Indicar carregamento|Consulta API|
|`ProgressBar`|Mostrar progresso|Download|
|`WebView`|Exibir conteúdo web|Página web|

---

# 15. Diferenças que você precisa saber

### Listas

```
CollectionView → lista moderna e flexível
ListView       → lista mais antiga
CarouselView   → lista em formato de carrossel
```

### Containers

```
Border → abordagem moderna
Frame  → abordagem mais antiga
```

### Carregamento

```
ActivityIndicator → "está carregando"
ProgressBar       → "está 60% concluído"
```

### Interação

```
SwipeView → deslizar para executar ações
RefreshView → puxar para atualizar
```

### Conteúdo externo

```
WebView → navegador incorporado no aplicativo
```

---

# 16. O que estudar e praticar

Para fixar essa parte do MAUI, eu recomendo praticar nesta ordem:

```
1. CollectionView
       ↓
2. ItemTemplate + DataTemplate
       ↓
3. Binding
       ↓
4. SelectionChanged
       ↓
5. Border
       ↓
6. SwipeView
       ↓
7. RefreshView
       ↓
8. ActivityIndicator
       ↓
9. ProgressBar
       ↓
10. CarouselView
       ↓
11. WebView
       ↓
12. Combinar tudo em uma tela real
```

**Os três conceitos mais importantes dessa etapa são `CollectionView`, `DataTemplate` e `Binding`**, porque eles formam a base para construir telas que exibem dados vindos de APIs, bancos de dados e outras fontes.