# 📱 .NET MAUI — Construção da Segunda Tela e ScrollView

Nesta aula, o professor dá continuidade à construção da interface do aplicativo Número da Sorte. O foco principal é aprender a:

- Reaproveitar a estrutura da primeira tela.
    
- Esconder elementos com `IsVisible`.
    
- Criar novas Labels.
    
- Centralizar textos e layouts.
    
- Organizar vários elementos horizontalmente com `HorizontalStackLayout`.
    
- Controlar espaçamento com `Spacing`.
    
- Trabalhar com `Margin`.
    
- Alterar `FontSize` e `TextColor`.
    
- Organizar a indentação do XAML.
    
- Utilizar `ScrollView` para permitir rolagem quando o conteúdo não couber na tela.
    

## 1. 🎯 Objetivo da aula

A primeira tela construída anteriormente possuía aproximadamente esta estrutura:

Plaintext

```
        [Imagem/Logo]

      Número da Sorte

          [BOTÃO]
```

Agora o professor começa a preparar uma segunda tela, que terá uma estrutura semelhante, mas exibirá o resultado:

Plaintext

```
        [Imagem/Logo]

      Número da Sorte:

     01   05   12   18   32   47

          Boa sorte!

          [BOTÃO]
```

A ideia importante é que não serão criadas duas páginas diferentes neste momento.

O professor pretende manter os elementos na mesma página e, posteriormente, controlar quais elementos ficam visíveis por meio de programação.

## 2. 🧠 Estratégia utilizada pelo professor

A estratégia é:

- **Construir as duas telas dentro da mesma estrutura e controlar a apresentação dos elementos posteriormente.**
    

Isso significa que, em vez de fazer:



```Plaintext
Página 1
   ↓
Página 2
```

ele pretende ter:

Plaintext

```
Uma única página
       ↓
 ┌───────────────┐
 │ Elementos     │
 │ da tela 1     │
 │               │
 │ Elementos     │
 │ da tela 2     │
 └───────────────┘
       ↓
Controlar
IsVisible
```

Isso será especialmente importante quando a lógica do aplicativo for implementada.

## 3. 👻 IsVisible: escondendo o número da sorte

O primeiro elemento que não deve aparecer na segunda tela é o número da sorte da primeira tela.

O professor utiliza:

XML

```
IsVisible="False"
```

Por exemplo:

XML

```
<Label
    Text="Número da Sorte"
    IsVisible="False" />
```

### O que significa?

|**Propriedade**|**Significado**|
|---|---|
|`IsVisible="True"`|Elemento aparece|
|`IsVisible="False"`|Elemento fica oculto|

É importante perceber que:

- `IsVisible="False"` não remove o elemento do XAML. Ele apenas faz com que o elemento não seja exibido.
    

Isso permite posteriormente fazer:

C#

```
minhaLabel.IsVisible = true;
```

ou:

C#

```
minhaLabel.IsVisible = false;
```

Isso será útil para controlar as diferentes etapas do aplicativo.

## 4. ⚠️ Um detalhe importante: margem de elemento escondido

O professor comenta que esconder uma Label pode trazer uma questão relacionada às margens.

Por exemplo:

XML

```
<Label
    Text="Número da Sorte"
    Margin="0,20,0,0"
    IsVisible="False" />
```

A margem pertence à própria Label.

Portanto, quando posteriormente forem feitas alterações na estrutura, é importante verificar qual elemento realmente deve possuir aquela margem.

A ideia principal é:

> Uma propriedade de layout deve ficar no elemento ao qual aquele espaçamento realmente pertence.

## 5. 🏷️ Criando a Label "Número da Sorte:"

Na segunda tela, o professor cria uma nova Label para representar o texto: `Número da Sorte:`

A estrutura é aproximadamente:

XML

```
<Label
    Text="Número da Sorte:"
    HorizontalOptions="Center" />
```

Aqui aparece uma propriedade muito importante: `HorizontalOptions="Center"`

## 6. ↔️ HorizontalOptions

Essa propriedade controla o posicionamento horizontal do elemento dentro do espaço disponível.

Exemplo:

XML

```
HorizontalOptions="Center"
```

significa: **Centralize horizontalmente este elemento.**

### Comparação

|**Valor**|**Efeito**|
|---|---|
|`Start`|Alinha à esquerda|
|`Center`|Centraliza|
|`End`|Alinha à direita|
|`Fill`|Ocupa o espaço disponível|

No contexto da aula:

XML

```
<Label
    Text="Número da Sorte:"
    HorizontalOptions="Center" />
```

faz com que o texto fique no centro da tela.

## 7. 🍀 Criando a mensagem "Boa sorte!"

O professor cria outra Label:

XML

```
<Label
    Text="Boa sorte!"
    HorizontalOptions="Center" />
```

Assim temos:

Plaintext

```
        Número da Sorte:

        01 05 12 18 32 47

             Boa sorte!
```

## 8. 📏 Utilizando Margin

A mensagem "Boa sorte!" precisa de um espaço maior em relação ao botão.

O professor utiliza uma margem inferior.

Exemplo:

XML

```
Margin="0,0,0,50"
```

A propriedade possui quatro valores:

`Margin="Esquerda, Superior, Direita, Inferior"`

Portanto: `Margin="0,0,0,50"` significa:

|**Posição**|**Valor**|
|---|---|
|Esquerda|0|
|Superior|0|
|Direita|0|
|Inferior|50|

Visualmente:

Plaintext

```
             Boa sorte!
                  ↓
              50 unidades
                  ↓
               [BOTÃO]
```

## 9. 📐 Ordem dos valores de Margin

Esse é um ponto importante para concursos e para desenvolvimento MAUI.

A sintaxe:

XML

```
Margin="left,top,right,bottom"
```

Pode ser memorizada como:

Plaintext

```
┌───────────────┐
│      TOP      │
│               │
│ LEFT      RIGHT
│               │
│    BOTTOM     │
└───────────────┘
```

Exemplo: `Margin="10,20,30,40"` significa:

- esquerda = 10
    
- superior = 20
    
- direita = 30
    
- inferior = 40
    

## 10. 🔢 Criando os números da sorte

Agora começa uma parte importante da aula.

O professor precisa criar seis números: `01`, `05`, `12`, `18`, `32`, `47`.

No exemplo mostrado durante a aula, ele começa utilizando várias Labels.

Algo semelhante a:

XML

```
<Label Text="01" />
<Label Text="01" />
<Label Text="01" />
<Label Text="01" />
<Label Text="01" />
<Label Text="01" />
```

Inicialmente, como elas estão dentro de um `VerticalStackLayout`, o resultado será:

Plaintext

```
01
01
01
01
01
01
```

Isso acontece porque o `VerticalStackLayout` organiza seus filhos verticalmente.

## 11. 📚 VerticalStackLayout

O `VerticalStackLayout` organiza os elementos em uma coluna.

Exemplo:

XML

```
<VerticalStackLayout>
    <Label Text="01" />
    <Label Text="05" />
    <Label Text="12" />
</VerticalStackLayout>
```

Resultado:

Plaintext

```
01
05
12
```

### Resumo

|**Layout**|**Organização**|
|---|---|
|`VerticalStackLayout`|Um abaixo do outro|
|`HorizontalStackLayout`|Um ao lado do outro|

## 12. ↔️ Solução: HorizontalStackLayout

Como os números precisam ficar lado a lado, o professor cria um `<HorizontalStackLayout>` e coloca as Labels dentro dele:


```XML
<HorizontalStackLayout>
    <Label Text="01" />
    <Label Text="05" />
    <Label Text="12" />
    <Label Text="18" />
    <Label Text="32" />
    <Label Text="47" />
</HorizontalStackLayout>
```

Agora o resultado passa a ser:

Plaintext

```
01 05 12 18 32 47
```

## 13. 🧩 Hierarquia dos elementos

Aqui aparece um conceito muito importante de XAML: hierarquia.

Temos:

```XML
<VerticalStackLayout>

    <Label />

    <HorizontalStackLayout>

        <Label />
        <Label />
        <Label />
        <Label />
        <Label />
        <Label />

    </HorizontalStackLayout>

    <Label />

</VerticalStackLayout>
```

Podemos representar assim:


```
VerticalStackLayout
│
├── Label
│
├── HorizontalStackLayout
│   ├── Label
│   ├── Label
│   ├── Label
│   ├── Label
│   ├── Label
│   └── Label
│
└── Label
```

Isso é extremamente importante para entender XAML.

## 14. ↪️ Indentação do XAML

O professor também explica a questão da indentação.

A indentação serve para tornar a hierarquia visualmente evidente.

Correto:



```XML
<VerticalStackLayout>

    <HorizontalStackLayout>

        <Label Text="01" />
        <Label Text="05" />

    </HorizontalStackLayout>

</VerticalStackLayout>
```

A indentação mostra claramente:

Plaintext

```
VerticalStackLayout
       ↓
HorizontalStackLayout
       ↓
     Label
```

Ela não altera o funcionamento do programa, mas melhora muito a legibilidade.

## 15. ⌨️ Atalhos para organizar o código

O professor mostra algumas formas de organizar a indentação.

### Formatação automática

No Visual Studio, pode-se utilizar: `Ctrl + K, Ctrl + D` (formata o documento).

Outra opção mencionada é selecionar o código e utilizar a combinação de formatação disponível no ambiente.

### Recuar / Avançar

- **Recuar:** `Shift + Tab`
    
- **Avançar:** `Tab`
    

|**Ação**|**Atalho**|
|---|---|
|Formatar documento|`Ctrl + K, Ctrl + D`|
|Aumentar indentação|`Tab`|
|Diminuir indentação|`Shift + Tab`|

## 16. 🟢 Alterando a cor dos números

Os números precisam ficar verdes.

O professor aproveita a mesma cor utilizada anteriormente no número da sorte.

A propriedade utilizada é `TextColor="Green"` ou, caso tenha sido definida uma cor específica, `TextColor="..."`.

Por exemplo:

```XML
<Label
    Text="01"
    TextColor="Green" />
```

Aplicando aos seis:

```XML
<Label Text="01" TextColor="Green" />
<Label Text="05" TextColor="Green" />
<Label Text="12" TextColor="Green" />
<Label Text="18" TextColor="Green" />
<Label Text="32" TextColor="Green" />
<Label Text="47" TextColor="Green" />
```

## 17. 🔠 Alterando o tamanho da fonte

O professor observa que as Labels estavam maiores do que no protótipo.

Ele altera o estilo geral das Labels utilizando `FontSize`.

Por exemplo:

```XML
<Style TargetType="Label">
    <Setter Property="FontSize" Value="12" />
</Style>
```

Isso faz com que as Labels tenham tamanho padrão 12.

## 18. 🎨 Estilo aplicado a todas as Labels

Esse conceito é muito importante.

Se você possui:

```XML
<Style TargetType="Label">
    <Setter Property="FontSize" Value="12" />
</Style>
```

o valor será aplicado às Labels correspondentes.

Podemos pensar:


```
Style
  │
  └── TargetType="Label"
           │
           ├── Label 1 → 12
           ├── Label 2 → 12
           ├── Label 3 → 12
           └── Label 4 → 12
```

Isso evita repetir `FontSize="12"` em cada Label.

## 19. 🔢 Exceção: número da sorte

Existe uma exceção.

Os números precisam ter tamanho maior: `FontSize="24"`.

Então, mesmo que o estilo geral determine `FontSize="12"`, podemos sobrescrever na própria Label:



```XML
<Label
    Text="01"
    FontSize="24" />
```

A propriedade local tem prioridade sobre o valor geral aplicado pelo estilo.

## 20. 🔤 Fonte utilizada

O professor também observa que o número possui uma fonte diferente.

A propriedade relacionada é `FontFamily`.

Por exemplo:


```XML
<Label
    Text="01"
    FontSize="24"
    FontFamily="OpenSansMedium" />
```

### Resumo das propriedades de texto

|**Propriedade**|**Função**|
|---|---|
|`FontSize`|Tamanho da fonte|
|`FontFamily`|Família/tipo da fonte|
|`TextColor`|Cor do texto|
|`Text`|Conteúdo textual|

## 21. 📦 Spacing do HorizontalStackLayout

Os números estavam inicialmente muito próximos: `010512183247`.

O professor utiliza `Spacing`. Essa propriedade controla o espaço entre os elementos filhos de um layout do tipo Stack.

Exemplo:

XML

```
<HorizontalStackLayout Spacing="10">
```

Resultado:

Plaintext

```
01   05   12   18   32   47
```

Se aumentar:

XML

```
<HorizontalStackLayout Spacing="20">
```

teremos ainda mais espaço:

Plaintext

```
01     05     12     18     32     47
```

## 22. 📊 Spacing × Margin

É importante não confundir os dois.

|**Propriedade**|**Atua sobre**|
|---|---|
|`Spacing`|Espaço entre os filhos de um StackLayout|
|`Margin`|Espaço externo de um determinado elemento|
|`Padding`|Espaço interno de um elemento/layout|

Exemplo:

- `<HorizontalStackLayout Spacing="10">` controla: `01 ←10→ 05 ←10→ 12`
    
- `<Label Margin="10,0,10,0"/>` controla a margem daquele elemento específico.
    

## 23. 🎯 Centralizando o HorizontalStackLayout

Depois de configurar os números, o professor centraliza o próprio layout:

```XML
<HorizontalStackLayout
    HorizontalOptions="Center"
    Spacing="10">
```

A diferença é importante:

- **Antes:** `HorizontalStackLayout` posicionado à esquerda com os elementos dentro.
    
- **Agora:** O próprio conjunto de números é centralizado:
    

Plaintext

```
             01  05  12  18  32  47
                    ↑
               centralizado
```

## 24. 📏 Margem do conjunto dos números

O professor adiciona margem ao `HorizontalStackLayout`.

Foi utilizado algo próximo de `Margin="0,70,0,70"`. A intenção é criar espaço acima e abaixo do conjunto:


```
Número da Sorte:

       ↓ espaço

01 05 12 18 32 47

       ↓ espaço

Boa sorte!
```

O valor exato utilizado durante a demonstração foi ajustado visualmente, chegando a aproximadamente 70.

## 25. 📜 O problema da tela pequena

Em determinado momento, o professor reduz o tamanho da tela e o conteúdo deixa de caber:


```
┌─────────────┐
│   imagem    │
│             │
│ Número...   │
│             │
│ 01 05 12... │
│             │
│ Boa sorte!  │
│             │
│ [BOTÃO]     │ ← conteúdo pode ficar fora
└─────────────┘
```

O problema é que o usuário não consegue acessar todo o conteúdo. Esse é um problema clássico de interfaces móveis.

## 26. 📜 Solução: ScrollView

A solução apresentada pelo professor é o `<ScrollView>`. O `ScrollView` permite que o conteúdo seja rolado quando não cabe completamente na área disponível.

## 27. 🧱 Como o ScrollView funciona?

O professor envolve o conteúdo existente.

**Antes:**



```XML
<VerticalStackLayout>
    ...
</VerticalStackLayout>
```

**Depois:**



```XML
<ScrollView>
    <VerticalStackLayout>
        ...
    </VerticalStackLayout>
</ScrollView>
```

A hierarquia passa a ser:

Plaintext

```
ScrollView
    │
    └── VerticalStackLayout
          │
          ├── Image
          ├── Label
          ├── HorizontalStackLayout
          ├── Label
          └── Button
```

## 28. ⚠️ Regra importante do ScrollView

O ponto principal é:

> O conteúdo que precisa ser rolado deve estar dentro do ScrollView.

Portanto, use:

```XML
<ScrollView>
    <VerticalStackLayout>
        ...
    </VerticalStackLayout>
</ScrollView>
```

e não simplesmente colocar o `ScrollView` solto dentro do layout quando a intenção é rolar a página inteira.

## 29. 🖱️ Comportamento do ScrollView

- **Quando a tela é suficientemente grande:** Não existe necessidade de rolagem.
    


```
┌────────────────────┐
│                    │
│      Conteúdo      │
│                    │
│      Conteúdo      │
│                    │
│      [BOTÃO]       │
│                    │
└────────────────────┘
```

- **Quando a tela fica pequena:** A rolagem fica disponível.
    


```
┌────────────────────┐
│ Conteúdo           │
│                    │
│ Conteúdo           │
│                    │
│ Conteúdo       █   │
│                 █  │
└────────────────────┘
```

## 30. 🧠 Conceitos fundamentais da aula

|**Conceito**|**Função**|
|---|---|
|`Label`|Exibir texto|
|`Text`|Define o conteúdo da Label|
|`IsVisible`|Controla se o elemento está visível|
|`HorizontalOptions`|Controla posicionamento horizontal|
|`Margin`|Define espaço externo|
|`FontSize`|Define tamanho da fonte|
|`FontFamily`|Define família da fonte|
|`TextColor`|Define cor do texto|
|`VerticalStackLayout`|Organiza elementos verticalmente|
|`HorizontalStackLayout`|Organiza elementos horizontalmente|
|`Spacing`|Define espaço entre filhos do Stack|
|`ScrollView`|Permite rolagem do conteúdo|

## 31. 🧩 Código completo da estrutura trabalhada

Como a transcrição não apresenta todos os elementos iniciais do arquivo XAML literalmente, o código abaixo consolida a estrutura construída na aula, preservando os valores e propriedades demonstrados pelo professor:



```XML
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="AppNumeroDaSorte.MainPage">

    <ScrollView>

        <VerticalStackLayout
            Padding="30,0"
            Spacing="25">

            <!-- Imagem / Logo -->
            <Image
                Source="logo.png"
                HeightRequest="185"
                Aspect="AspectFit"
                SemanticProperties.Description="Número da Sorte" />

            <!-- Elemento da primeira tela, ocultado -->
            <Label
                Text="Número da Sorte"
                IsVisible="False" />

            <!-- Título da segunda tela -->
            <Label
                Text="Número da Sorte:"
                HorizontalOptions="Center"
                Margin="0,20,0,0" />

            <!-- Números sorteados -->
            <HorizontalStackLayout
                HorizontalOptions="Center"
                Spacing="10"
                Margin="0,70,0,70">

                <Label
                    Text="01"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="05"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="12"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="18"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="32"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

                <Label
                    Text="47"
                    FontSize="24"
                    FontFamily="OpenSansMedium"
                    TextColor="Green" />

            </HorizontalStackLayout>

            <!-- Mensagem -->
            <Label
                Text="Boa sorte!"
                HorizontalOptions="Center"
                Margin="0,0,0,50" />

            <!-- Botão -->
            <Button
                Text="Gerar número da sorte" />

        </VerticalStackLayout>

    </ScrollView>

</ContentPage>
```

> **Observação:** os valores de `Padding`, `HeightRequest`, `Source` e alguns detalhes da primeira tela não aparecem integralmente na transcrição. Portanto, o código acima é uma reconstrução completa da estrutura demonstrada, não uma reprodução literal de cada linha do projeto do professor.

## 32. 🎨 Exemplo de estilo global para Label

A aula também demonstra a alteração do tamanho padrão das Labels pelo estilo. Uma estrutura possível é:



```XML
<ContentPage.Resources>

    <Style TargetType="Label">

        <Setter
            Property="FontSize"
            Value="12" />

    </Style>

</ContentPage.Resources>
```

Assim, todas as Labels passam a utilizar `FontSize = 12`, exceto aquelas que sobrescrevem o valor:



```XML
<Label
    Text="01"
    FontSize="24" />
```

## 33. 🔥 O que você deve memorizar desta aula

Para fins de estudo, especialmente pensando em programação e concursos, concentre-se nestes pontos:

- **IsVisible:** `IsVisible="False"` → Esconde o elemento.
    
- **HorizontalOptions:** `HorizontalOptions="Center"` → Centraliza horizontalmente.
    
- **Margin:** `Margin="0,20,0,0"` → Ordem: Esquerda, Superior, Direita, Inferior.
    
- **VerticalStackLayout:** `<VerticalStackLayout>` → Elementos organizados verticalmente.
    
- **HorizontalStackLayout:** `<HorizontalStackLayout>` → Elementos organizados horizontalmente.
    
- **Spacing:** `Spacing="10"` → Espaço entre os elementos filhos.
    
- **FontSize:** `FontSize="24"` → Tamanho da fonte.
    
- **FontFamily:** `FontFamily="OpenSansMedium"` → Família da fonte.
    
- **TextColor:** `TextColor="Green"` → Cor do texto.
    
- **ScrollView:** Envolve a estrutura (`<ScrollView><VerticalStackLayout>...</VerticalStackLayout></ScrollView>`) → Permite rolar o conteúdo quando ele não cabe na área disponível.
    

## 34. 🧠 Mapa mental da aula



```Plaintext
SEGUNDA TELA
│
├── Reaproveitar estrutura
│
├── Ocultar elementos
│   └── IsVisible="False"
│
├── Criar Labels
│   ├── Número da Sorte:
│   └── Boa sorte!
│
├── Posicionamento
│   └── HorizontalOptions="Center"
│
├── Espaçamento
│   ├── Margin
│   └── Spacing
│
├── Números
│   └── HorizontalStackLayout
│       ├── 01
│       ├── 05
│       ├── 12
│       ├── 18
│       ├── 32
│       └── 47
│
├── Aparência
│   ├── FontSize
│   ├── FontFamily
│   └── TextColor
│
├── Organização do código
│   └── Indentação
│
└── Conteúdo maior que a tela
    └── ScrollView
```

## 🎯 Essência da aula

A grande ideia desta etapa é aprender que XAML não serve apenas para colocar componentes na tela. Ele permite estruturar hierarquicamente a interface e controlar posição, espaçamento, aparência, visibilidade e rolagem.

A estrutura mais importante que aparece na aula é:



```XML
<ScrollView>

    <VerticalStackLayout>

        <Label />

        <HorizontalStackLayout
            HorizontalOptions="Center"
            Spacing="10">

            <Label />
            <Label />
            <Label />
            <Label />
            <Label />
            <Label />

        </HorizontalStackLayout>

        <Label />

        <Button />

    </VerticalStackLayout>

</ScrollView>
```

Se você entender essa hierarquia, já terá captado o principal da aula:

- `ScrollView` contém o conteúdo rolável
    
- `VerticalStackLayout` organiza as seções verticalmente
    
- `HorizontalStackLayout` organiza os números horizontalmente
    
- `Labels` representam os textos e números.


### 📱 Tabela — Conceitos e exemplos da aula

| Conceito                    | Para que serve                                       | Exemplo                                               | Resultado                                        |
| --------------------------- | ---------------------------------------------------- | ----------------------------------------------------- | ------------------------------------------------ |
| **`Label`**                 | Exibir textos na tela                                | `<Label Text="Boa sorte!" />`                         | Exibe o texto **Boa sorte!**                     |
| **`Text`**                  | Define o conteúdo textual de uma `Label`             | `Text="Número da Sorte:"`                             | Mostra **Número da Sorte:**                      |
| **`IsVisible`**             | Controla se um elemento aparece ou fica oculto       | `IsVisible="False"`                                   | O elemento fica invisível                        |
| **`HorizontalOptions`**     | Define o posicionamento horizontal                   | `HorizontalOptions="Center"`                          | Centraliza o elemento horizontalmente            |
| **`Margin`**                | Define espaço **externo** ao elemento                | `Margin="0,0,0,50"`                                   | Cria 50 unidades de espaço abaixo                |
| **`Spacing`**               | Define espaço entre os filhos de um Stack            | `Spacing="10"`                                        | Cria 10 unidades entre cada elemento             |
| **`VerticalStackLayout`**   | Organiza elementos verticalmente                     | `<VerticalStackLayout>`                               | Elementos ficam um abaixo do outro               |
| **`HorizontalStackLayout`** | Organiza elementos horizontalmente                   | `<HorizontalStackLayout>`                             | Elementos ficam lado a lado                      |
| **`ScrollView`**            | Permite rolar o conteúdo quando ele não cabe na tela | `<ScrollView>...</ScrollView>`                        | Usuário pode deslizar para visualizar o restante |
| **`FontSize`**              | Define o tamanho da fonte                            | `FontSize="24"`                                       | Texto fica maior                                 |
| **`FontFamily`**            | Define a família/tipo da fonte                       | `FontFamily="OpenSansMedium"`                         | Utiliza a fonte especificada                     |
| **`TextColor`**             | Define a cor do texto                                | `TextColor="Green"`                                   | Texto fica verde                                 |
| **`Style`**                 | Permite definir propriedades padrão para elementos   | `<Style TargetType="Label">`                          | Aplica configurações às `Label`s                 |
| **`Setter`**                | Define uma propriedade dentro de um `Style`          | `<Setter Property="FontSize" Value="12" />`           | Define `FontSize=12` como padrão                 |
| **Hierarquia XAML**         | Organiza elementos dentro de outros elementos        | `VerticalStackLayout → HorizontalStackLayout → Label` | Define a estrutura da interface                  |
| **Indentação**              | Facilita a visualização da hierarquia                | Elementos filhos ficam recuados                       | Código fica mais legível                         |

Os conceitos de `Label`, `IsVisible`, `HorizontalOptions`, `Margin`, `FontSize`, `FontFamily`, `TextColor`, `VerticalStackLayout`, `HorizontalStackLayout`, `Spacing` e `ScrollView` são explicitamente destacados como fundamentais na aula.

### 🔹 Exemplos principais da aula

|Situação|Código|O que acontece|
|---|---|---|
|Esconder uma `Label`|`<Label Text="Número da Sorte" IsVisible="False" />`|A `Label` não é exibida|
|Centralizar texto|`<Label Text="Número da Sorte:" HorizontalOptions="Center" />`|Texto fica centralizado|
|Criar números lado a lado|`<HorizontalStackLayout Spacing="10">`|Os números ficam horizontalmente organizados|
|Criar espaçamento inferior|`Margin="0,0,0,50"`|Cria espaço abaixo do elemento|
|Aumentar fonte|`FontSize="24"`|Texto fica maior|
|Alterar fonte|`FontFamily="OpenSansMedium"`|Utiliza a família de fonte indicada|
|Alterar cor|`TextColor="Green"`|Texto fica verde|
|Permitir rolagem|`<ScrollView><VerticalStackLayout>...</VerticalStackLayout></ScrollView>`|Conteúdo pode ser rolado|
|Aplicar estilo às Labels|`<Style TargetType="Label">`|Define propriedades padrão para as Labels|
|Sobrescrever estilo|`<Label Text="01" FontSize="24" />`|Essa Label usa 24 em vez do tamanho padrão|

### 🧠 Pontos para memorizar

|Se você encontrar...|Lembre-se de...|
|---|---|
|`IsVisible`|**Visibilidade**|
|`HorizontalOptions`|**Posicionamento horizontal**|
|`Margin`|**Espaço externo**|
|`Spacing`|**Espaço entre filhos**|
|`VerticalStackLayout`|**Vertical**|
|`HorizontalStackLayout`|**Horizontal**|
|`FontSize`|**Tamanho da fonte**|
|`FontFamily`|**Família da fonte**|
|`TextColor`|**Cor do texto**|
|`ScrollView`|**Rolagem**|
|`Style`|**Configuração padrão**|
|`Setter`|**Define uma propriedade do estilo**|