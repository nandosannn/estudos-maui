# 3. Layouts no .NET MAUI

> **Objetivo:** entender como organizar, dimensionar, posicionar e distribuir elementos visuais em uma interface .NET MAUI.

---

## 📑 Índice

1. [[#1. Conceito de Layout]]
    
2. [[#2. Principais Layouts]]
    
    - [[#2.1 VerticalStackLayout]]
        
    - [[#2.2 HorizontalStackLayout]]
        
    - [[#2.3 Grid]]
        
    - [[#2.4 FlexLayout]]
        
    - [[#2.5 ScrollView]]
        
    - [[#2.6 AbsoluteLayout]]
        
3. [[#3. Dimensionamento e distribuição]]
    
    - [[#3.1 Padding]]
        
    - [[#3.2 Margin]]
        
    - [[#3.3 Spacing]]
        
    - [[#3.4 WidthRequest]]
        
    - [[#3.5 HeightRequest]]
        
4. [[#4. Alinhamento]]
    
    - [[#4.1 HorizontalOptions]]
        
    - [[#4.2 VerticalOptions]]
        
5. [[#5. Grid — Estrutura]]
    
    - [[#5.1 RowDefinitions]]
        
    - [[#5.2 ColumnDefinitions]]
        
    - [[#5.3 Grid.Row]]
        
    - [[#5.4 Grid.Column]]
        
    - [[#5.5 Auto]]
        
    - [[#5.6 *]]
        
    - [[#5.7 Proporções]]
        
    - [[#5.8 RowSpan e ColumnSpan]]
        
6. [[#6. FlexLayout — Distribuição]]
    
    - [[#6.1 Direction]]
        
    - [[#6.2 JustifyContent]]
        
7. [[#7. ScrollView — Rolagem]]
    
8. [[#8. AbsoluteLayout — Posicionamento]]
    
9. [[#9. Aninhamento de Layouts]]
    
10. [[#10. Como escolher o Layout]]
    
11. [[#11. Diferenças fundamentais]]
    
12. [[#12. Mapa mental para prova]]
    

---

# 1. Conceito de Layout

**Layout** é o mecanismo responsável por organizar os elementos filhos dentro de um espaço.

Os layouts determinam:

- onde os elementos ficam;
    
- quanto espaço ocupam;
    
- como os elementos são distribuídos;
    
- como os elementos se relacionam entre si.
    

---

# 2. Principais Layouts

|Layout|Organização|Principal uso|
|---|---|---|
|`VerticalStackLayout`|Vertical|Empilhar elementos|
|`HorizontalStackLayout`|Horizontal|Elementos lado a lado|
|`Grid`|Linhas e colunas|Estruturas complexas|
|`FlexLayout`|Flexível|Distribuição semelhante ao Flexbox|
|`ScrollView`|Rolagem|Conteúdo maior que a tela|
|`AbsoluteLayout`|Posicional|Posicionamento específico|

---

## 2.1 `VerticalStackLayout`

Organiza os elementos **verticalmente**.

```text
Elemento 1
    ↓
Elemento 2
    ↓
Elemento 3
```

**Usos:**

- formulários;
    
- telas de login;
    
- menus;
    
- páginas simples;
    
- sequências de informações.
    

```xml
<VerticalStackLayout>
    <Label Text="Nome" />
    <Entry />
    <Button Text="Enviar" />
</VerticalStackLayout>
```

---

## 2.2 `HorizontalStackLayout`

Organiza os elementos **horizontalmente**.

```text
Elemento 1 → Elemento 2 → Elemento 3
```

**Usos:**

- botões lado a lado;
    
- ícone + texto;
    
- barras de ações;
    
- informações resumidas.
    

```xml
<HorizontalStackLayout Spacing="10">
    <Button Text="Editar" />
    <Button Text="Excluir" />
</HorizontalStackLayout>
```

---

## 2.3 `Grid`

Organiza elementos utilizando **linhas e colunas**.

```text
┌──────────┬──────────┐
│          │          │
│  Row 0   │  Row 0   │
├──────────┼──────────┤
│          │          │
│  Row 1   │  Row 1   │
└──────────┴──────────┘
 Col 0        Col 1
```

É especialmente útil para:

- formulários;
    
- estruturas de linhas e colunas;
    
- interfaces mais complexas;
    
- distribuição proporcional de espaço.
    

---

## 2.4 `FlexLayout`

Permite uma **distribuição flexível** dos elementos, baseada no conceito de Flexbox.

Pode controlar:

- direção;
    
- alinhamento;
    
- distribuição;
    
- quebra de linha;
    
- crescimento;
    
- encolhimento.
    

```xml
<FlexLayout
    Direction="Row"
    JustifyContent="SpaceBetween">

    <Button Text="Um" />
    <Button Text="Dois" />
    <Button Text="Três" />

</FlexLayout>
```

---

## 2.5 `ScrollView`

Permite **rolar o conteúdo** quando ele não cabe na tela.

```xml
<ScrollView>
    <VerticalStackLayout>
        ...
    </VerticalStackLayout>
</ScrollView>
```

### Regra importante

Um `ScrollView` normalmente possui **um único filho direto**.

É comum utilizar:

```text
ScrollView
    └── VerticalStackLayout
            ├── Elemento
            ├── Elemento
            └── Elemento
```

---

## 2.6 `AbsoluteLayout`

Permite posicionar elementos utilizando **coordenadas e proporções relativas ao espaço disponível**.

```xml
<AbsoluteLayout>

    <BoxView
        AbsoluteLayout.LayoutBounds="0,0,100,100" />

</AbsoluteLayout>
```

`LayoutBounds` representa:

```text
X, Y, Width, Height
```

**Usos:**

- sobreposição;
    
- elementos flutuantes;
    
- badges;
    
- componentes sobre imagens;
    
- posicionamento específico.
    

---

# 3. Dimensionamento e distribuição

## 3.1 `Padding`

Define o **espaço interno** entre a borda do elemento/layout e seu conteúdo.

```xml
<VerticalStackLayout Padding="20">
```

### Forma de memorizar

> **Padding = dentro**

### Valores

```xml
Padding="20"
```

Todos os lados.

```xml
Padding="20,10"
```

```text
Horizontal = 20
Vertical   = 10
```

```xml
Padding="10,20,30,40"
```

Ordem:

```text
Left → Top → Right → Bottom
```

---

## 3.2 `Margin`

Define o **espaço externo** ao redor do elemento.

```xml
<Label
    Text="Nome"
    Margin="20" />
```

### Forma de memorizar

> **Margin = fora**

---

## 3.3 `Spacing`

Define o espaço **entre os elementos filhos** de um `StackLayout`.

```xml
<VerticalStackLayout Spacing="20">
```

```text
Elemento 1

   ← 20 →

Elemento 2

   ← 20 →

Elemento 3
```

### Forma de memorizar

> **Spacing = entre**

---

## 3.4 `WidthRequest`

Define a **largura desejada** de um elemento.

```xml
<Button
    Text="Entrar"
    WidthRequest="200" />
```

> **WidthRequest = largura solicitada**

---

## 3.5 `HeightRequest`

Define a **altura desejada** de um elemento.

```xml
<Button
    Text="Entrar"
    HeightRequest="60" />
```

> **HeightRequest = altura solicitada**

### Atenção

`WidthRequest` e `HeightRequest` representam **tamanhos solicitados**, não necessariamente uma garantia absoluta de tamanho.

---

# 4. Alinhamento

## 4.1 `HorizontalOptions`

Controla o **posicionamento horizontal** do elemento.

|Valor|Significado|
|---|---|
|`Start`|Início|
|`Center`|Centro|
|`End`|Final|
|`Fill`|Preencher espaço disponível|

Exemplo:

```xml
<Button
    Text="Entrar"
    HorizontalOptions="Center" />
```

---

## 4.2 `VerticalOptions`

Controla o **posicionamento vertical**.

|Valor|Significado|
|---|---|
|`Start`|Topo/início|
|`Center`|Centro|
|`End`|Final/baixo|
|`Fill`|Preencher|

Exemplo:

```xml
<Label
    Text="Olá"
    VerticalOptions="Center" />
```

---

# 5. Grid — Estrutura

O `Grid` trabalha principalmente com:

```text
Rows    → linhas
Columns → colunas
```

---

## 5.1 `RowDefinitions`

Define as **linhas**.

```xml
<Grid.RowDefinitions>

    <RowDefinition Height="100" />

    <RowDefinition Height="*" />

    <RowDefinition Height="50" />

</Grid.RowDefinitions>
```

---

## 5.2 `ColumnDefinitions`

Define as **colunas**.

```xml
<Grid.ColumnDefinitions>

    <ColumnDefinition Width="100" />

    <ColumnDefinition Width="*" />

</Grid.ColumnDefinitions>
```

---

## 5.3 `Grid.Row`

Indica em qual **linha** o elemento será colocado.

```xml
<Label
    Text="Nome"
    Grid.Row="0" />
```

Os índices começam em **zero**.

```text
Row 0 → primeira linha
Row 1 → segunda linha
Row 2 → terceira linha
```

---

## 5.4 `Grid.Column`

Indica em qual **coluna** o elemento será colocado.

```xml
<Entry
    Grid.Column="1" />
```

```text
Column 0 → primeira coluna
Column 1 → segunda coluna
Column 2 → terceira coluna
```

---

## 5.5 `Auto`

O tamanho é determinado de acordo com o **conteúdo**.

```xml
<RowDefinition Height="Auto" />
```

### Memorize

> **Auto = tamanho necessário para o conteúdo**

---

## 5.6 `*`

Representa o **espaço restante disponível**.

```xml
<ColumnDefinition Width="*" />
```

Duas colunas:

```xml
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
```

Dividem o espaço igualmente:

```text
┌──────────────┬──────────────┐
│     50%      │     50%      │
└──────────────┴──────────────┘
```

---

## 5.7 Proporções

Podemos utilizar valores como:

```xml
<ColumnDefinition Width="2*" />
<ColumnDefinition Width="1*" />
```

Significa:

```text
2 : 1
```

A primeira coluna recebe duas partes e a segunda uma parte.

```text
┌───────────────────────┬───────────┐
│         2*            │    1*     │
└───────────────────────┴───────────┘
```

---

## 5.8 `RowSpan` e `ColumnSpan`

Permitem que um elemento ocupe várias linhas ou colunas.

### `ColumnSpan`

```xml
<Button
    Grid.Column="0"
    Grid.ColumnSpan="2"
    Text="Cadastrar" />
```

O elemento ocupa **duas colunas**.

### `RowSpan`

```xml
<Label
    Grid.Row="0"
    Grid.RowSpan="2"
    Text="Informação" />
```

O elemento ocupa **duas linhas**.

---

# 6. FlexLayout — Distribuição

## 6.1 `Direction`

Determina a direção dos elementos.

### `Row`

Horizontal:

```text
→ → →
```

```xml
Direction="Row"
```

### `Column`

Vertical:

```text
↓
↓
↓
```

```xml
Direction="Column"
```

---

## 6.2 `JustifyContent`

Controla a distribuição dos elementos no **eixo principal**.

|Valor|Comportamento|
|---|---|
|`Start`|Início|
|`Center`|Centro|
|`End`|Final|
|`SpaceBetween`|Espaço entre elementos|
|`SpaceAround`|Espaço ao redor|
|`SpaceEvenly`|Espaços iguais|

Exemplo:

```xml
JustifyContent="SpaceBetween"
```

```text
┌──────────────────────────────┐
│ A          B          C      │
└──────────────────────────────┘
```

---

# 7. ScrollView — Rolagem

Usado quando o conteúdo pode ser **maior que o espaço disponível**.

```xml
<ScrollView>
    <VerticalStackLayout>
        ...
    </VerticalStackLayout>
</ScrollView>
```

### Palavra-chave

> **ScrollView = rolagem**

---

# 8. AbsoluteLayout — Posicionamento

Permite posicionamento baseado em:

```text
X
Y
Width
Height
```

Exemplo:

```xml
AbsoluteLayout.LayoutBounds="0,0,100,100"
```

### Palavra-chave

> **AbsoluteLayout = posicionamento específico**

Não deve ser a primeira escolha para layouts comuns; `Grid`, `VerticalStackLayout` e `FlexLayout` normalmente são mais adequados para interfaces adaptáveis.

---

# 9. Aninhamento de Layouts

Layouts podem ser colocados **dentro de outros layouts**.

Exemplo:

```text
ScrollView
    │
    └── VerticalStackLayout
            │
            ├── Label
            ├── Entry
            ├── Button
            │
            └── HorizontalStackLayout
                    ├── Label
                    └── Label
```

Isso permite construir interfaces mais complexas combinando diferentes layouts.

---

# 10. Como escolher o Layout

|Necessidade|Layout|
|---|---|
|Elementos um abaixo do outro|`VerticalStackLayout`|
|Elementos lado a lado|`HorizontalStackLayout`|
|Linhas e colunas|`Grid`|
|Distribuição flexível|`FlexLayout`|
|Conteúdo rolável|`ScrollView`|
|Posicionamento específico/sobreposição|`AbsoluteLayout`|

---

# 11. Diferenças fundamentais

## `Padding` × `Margin` × `Spacing`

|Conceito|Onde atua?|Palavra-chave|
|---|---|---|
|`Padding`|Dentro do elemento|**Interno**|
|`Margin`|Fora do elemento|**Externo**|
|`Spacing`|Entre elementos filhos|**Entre**|

### Regra de memorização

> **Padding = dentro**  
> **Margin = fora**  
> **Spacing = entre**

---

## `WidthRequest` × `HeightRequest`

|Conceito|Controla|
|---|---|
|`WidthRequest`|Largura desejada|
|`HeightRequest`|Altura desejada|

---

## `HorizontalOptions` × `VerticalOptions`

|Conceito|Controla|
|---|---|
|`HorizontalOptions`|Alinhamento horizontal|
|`VerticalOptions`|Alinhamento vertical|

---

# 12. Mapa mental para prova

```text
LAYOUTS — .NET MAUI
│
├── ORGANIZAÇÃO
│   │
│   ├── VerticalStackLayout
│   │   └── ↓ ↓ ↓
│   │
│   ├── HorizontalStackLayout
│   │   └── → → →
│   │
│   ├── Grid
│   │   └── Linhas + Colunas
│   │
│   ├── FlexLayout
│   │   └── Distribuição flexível
│   │
│   ├── ScrollView
│   │   └── Rolagem
│   │
│   └── AbsoluteLayout
│       └── Posicionamento
│
├── ESPAÇAMENTO
│   │
│   ├── Padding
│   │   └── Dentro
│   │
│   ├── Margin
│   │   └── Fora
│   │
│   └── Spacing
│       └── Entre filhos
│
├── TAMANHO
│   │
│   ├── WidthRequest
│   │   └── Largura desejada
│   │
│   └── HeightRequest
│       └── Altura desejada
│
├── ALINHAMENTO
│   │
│   ├── HorizontalOptions
│   │   └── Horizontal
│   │
│   └── VerticalOptions
│       └── Vertical
│
└── GRID
    │
    ├── RowDefinitions
    │   └── Linhas
    │
    ├── ColumnDefinitions
    │   └── Colunas
    │
    ├── Grid.Row
    │   └── Linha
    │
    ├── Grid.Column
    │   └── Coluna
    │
    ├── Auto
    │   └── Tamanho do conteúdo
    │
    ├── *
    │   └── Espaço restante
    │
    ├── 2*, 3*, ...
    │   └── Proporção
    │
    ├── RowSpan
    │   └── Ocupa várias linhas
    │
    └── ColumnSpan
        └── Ocupa várias colunas
```

---

## 🧠 Resumo de 30 segundos

| Se a questão falar em...       | Pense em...             |
| ------------------------------ | ----------------------- |
| Empilhar verticalmente         | `VerticalStackLayout`   |
| Organizar horizontalmente      | `HorizontalStackLayout` |
| Linhas e colunas               | `Grid`                  |
| Flexbox                        | `FlexLayout`            |
| Rolagem                        | `ScrollView`            |
| Coordenadas/posição específica | `AbsoluteLayout`        |
| Espaço interno                 | `Padding`               |
| Espaço externo                 | `Margin`                |
| Espaço entre filhos            | `Spacing`               |
| Largura                        | `WidthRequest`          |
| Altura                         | `HeightRequest`         |
| Alinhamento horizontal         | `HorizontalOptions`     |
| Alinhamento vertical           | `VerticalOptions`       |
| Definir linhas                 | `RowDefinitions`        |
| Definir colunas                | `ColumnDefinitions`     |
| Tamanho conforme conteúdo      | `Auto`                  |
| Espaço restante                | `*`                     |
| Distribuição proporcional      | `2*`, `3*`...           |
| Ocupa várias colunas           | `ColumnSpan`            |
| Ocupa várias linhas            | `RowSpan`               |