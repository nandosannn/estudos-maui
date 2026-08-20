# 📱 .NET MAUI — Border e estilização dos números da sorte

Nesta aula, o professor finaliza a parte visual da segunda tela do aplicativo Número da Sorte. O objetivo é transformar cada número em um pequeno cartão com borda colorida e cantos arredondados, preparando a interface para a próxima etapa, em que os números serão gerados dinamicamente pelo código.

A estrutura visual que o professor busca é aproximadamente:

Plaintext

```
        Número da Sorte:

    ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐
    │ 01 │ │ 05 │ │ 12 │ │ 18 │ │ 32 │ │ 47 │
    └────┘ └────┘ └────┘ └────┘ └────┘ └────┘

                 Boa sorte!
```

## 1. 🎯 Objetivo da aula

O professor trabalha principalmente com:

- `Border`
    
- `Stroke`
    
- `StrokeShape`
    
- `Padding`
    
- `RoundRectangle`
    
- `CornerRadius`
    
- `Spacing`
    
- Organização de elementos no XAML
    

O objetivo é sair de:

Plaintext

```
01  05  12  18  32  47
```

para:

Plaintext

```
┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐
│ 01 │ │ 05 │ │ 12 │ │ 18 │ │ 32 │ │ 47 │
└────┘ └────┘ └────┘ └────┘ └────┘ └────┘
```

## 2. 🧱 O componente Border

O principal recurso apresentado é o componente:

XML

```
<Border>
```

O `Border` permite colocar uma borda ao redor de um elemento. No caso da aula, cada número terá sua própria borda.

A estrutura conceitual é:

Plaintext

```
Border
  │
  └── Label
       └── "01"
```

Ou seja:

XML

```
<Border>
    <Label Text="01" />
</Border>
```

## 3. 📦 Um Border precisa envolver um elemento

O professor destaca que o `Border` é utilizado envolvendo o conteúdo que queremos destacar.

Por exemplo:

XML

```
<Border>
    <Label Text="01" />
</Border>
```

Visualmente:

Plaintext

```
┌─────────┐
│   01    │
└─────────┘
```

No aplicativo teremos seis estruturas semelhantes:

- Border → Label 01
    
- Border → Label 05
    
- Border → Label 12
    
- Border → Label 18
    
- Border → Label 32
    
- Border → Label 47
    

## 4. 🎨 Stroke: cor da borda

Depois de criar o `Border`, o professor altera a cor da borda utilizando a propriedade `Stroke` com a cor `#00AB37`:

XML

```
<Border Stroke="#00AB37">
```

A propriedade `Stroke` representa o traço/borda do elemento.

### Resumo

|**Propriedade**|**Função**|
|---|---|
|`Stroke`|Define a cor da borda|
|`StrokeShape`|Define o formato da borda|
|`Padding`|Espaçamento interno|
|`Margin`|Espaçamento externo|

## 5. 📐 Padding: margem interna

O professor utiliza `Padding` para criar espaço entre a borda e o número.

Por exemplo:

XML

```
Padding="5"
```

Temos:

Plaintext

```
┌─────────────┐
│             │
│     01      │
│             │
└─────────────┘
```

O `Padding` cria espaço dentro do componente.

## 6. ⚠️ Padding × Margin

Essa diferença é muito importante.

### Padding

É o espaço interno.

Plaintext

```
┌─────────────────┐
│   ← PADDING →   │
│      LABEL      │
│   ← PADDING →   │
└─────────────────┘
```

### Margin

É o espaço externo.

Plaintext

```
       ← MARGIN →

   ┌─────────────┐
   │    LABEL    │
   └─────────────┘

       ← MARGIN →
```

|**Propriedade**|**Espaço**|
|---|---|
|`Padding`|Entre o conteúdo e a borda|
|`Margin`|Entre o elemento e os elementos vizinhos|

## 7. 📏 Ajustando o Padding

O professor inicialmente coloca:

XML

```
Padding="5"
```

Isso significa aproximadamente:

- esquerda = 5
    
- superior = 5
    
- direita = 5
    
- inferior = 5
    

Mas ele percebe que o espaço horizontal não ficou ideal. Por isso, utiliza valores diferentes:

XML

```
Padding="10,5"
```

Nesse formato:

- **Horizontal:** 10
    
- **Vertical:** 5
    

Ou seja:

Plaintext

```
       10        10
    ←─────→   ←─────→

       ┌────────────┐
    5  │     01     │  5
       └────────────┘
```

Isso deixa o cartão mais largo sem aumentar excessivamente sua altura.

## 8. 🧠 Sintaxe resumida do Padding

O XAML permite diferentes formas de informar valores.

### Um valor

XML

```
Padding="5"
```

Aplica o mesmo valor em todos os lados:

Plaintext

```
5
5   conteúdo   5
5
```

### Dois valores

XML

```
Padding="10,5"
```

Representa:

- horizontal = 10
    
- vertical = 5
    

### Quatro valores

XML

```
Padding="10,5,20,15"
```

Segue a ordem: `Left, Top, Right, Bottom`

## 9. 🔲 Arredondando os cantos

Depois de criar a borda, o professor percebe que falta o arredondamento.

A propriedade apresentada é `StrokeShape`, que permite definir o formato da borda:

XML

```
StrokeShape="RoundRectangle"
```

Isso transforma a borda em um retângulo com cantos arredondados.

## 10. 🔵 RoundRectangle

O `RoundRectangle` significa: **Retângulo com cantos arredondados.**

Exemplo:

XML

```
<Border
    Stroke="#00AB37"
    StrokeShape="RoundRectangle">
    
    <Label Text="01" />

</Border>
```

Visualmente:

Plaintext

```
╭──────────╮
│    01    │
╰──────────╯
```

## 11. 📐 Controlando o arredondamento

O professor mostra que é possível definir o raio dos cantos utilizando `RoundRectangle CornerRadius="8"` ou `RoundRectangle 8`:

XML

```
<Border
    Stroke="#00AB37"
    StrokeShape="RoundRectangle 8">
```

A ideia é: `8 → raio do arredondamento`. Quanto maior o valor, mais arredondados ficam os cantos:

Plaintext

```
5                     15
╭────────╮            ╭────────────╮
│   01   │   versus   │     01     │
╰────────╯            ╰────────────╯
```

## 12. 🎛️ Arredondamento individual dos cantos

O professor também explica que é possível controlar individualmente os quatro cantos utilizando valores diferentes: `5, 10, 20, 30`.

A ordem segue os quatro cantos do retângulo, permitindo produzir efeitos como:

Plaintext

```
╭───────────────╮
│               ╲
│       01       ╲
╲                 │
 ╲────────────────╯
```

Embora isso não seja necessário para o aplicativo, é importante conhecer a possibilidade.

## 13. 🧩 Estrutura básica do Border

A estrutura que você deve memorizar é:

XML

```
<Border
    Stroke="#00AB37"
    StrokeShape="RoundRectangle 8"
    Padding="10,5">

    <Label
        Text="01"
        FontSize="24"
        TextColor="#00AB37" />

</Border>
```

Temos:

Plaintext

```
Border
│
├── Stroke
│      └── cor da borda
│
├── StrokeShape
│      └── formato
│
├── Padding
│      └── espaço interno
│
└── Label
       └── número
```

## 14. 🔢 Criando os seis números

O professor copia o primeiro `Border` para os demais números. A estrutura passa a ser:

Plaintext

```
HorizontalStackLayout
│
├── Border
│   └── Label "01"
│
├── Border
│   └── Label "05"
│
├── Border
│   └── Label "12"
│
├── Border
│   └── Label "18"
│
├── Border
│   └── Label "32"
│
└── Border
    └── Label "47"
```

Anteriormente tínhamos:

`HorizontalStackLayout → [Label, Label, Label, Label, Label, Label]`

Agora temos:

`HorizontalStackLayout → [Border → Label, Border → Label, ...]`

## 15. ↔️ Spacing

Depois de criar as seis bordas, o professor percebe que elas estão muito afastadas e reduz o `Spacing` do `HorizontalStackLayout`:

XML

```
<HorizontalStackLayout
    Spacing="5">
```

O resultado é:

Plaintext

```
┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐
│ 01 │ │ 05 │ │ 12 │ │ 18 │ │ 32 │ │ 47 │
└────┘ └────┘ └────┘ └────┘ └────┘ └────┘
```

## 16. 🆚 Spacing e Padding juntos

Esse é um ponto excelente para memorizar:

XML

```
<HorizontalStackLayout Spacing="5">

    <Border Padding="10,5">
        <Label Text="01" />
    </Border>

    <Border Padding="10,5">
        <Label Text="05" />
    </Border>

</HorizontalStackLayout>
```

Temos dois tipos de espaço:

Plaintext

```
        SPACING
   ←──────────────→

  ╭────────╮      ╭────────╮
  │  PADDING│      │ PADDING│
  │   01   │      │   05   │
  ╰────────╯      ╰────────╯
```

- **Padding:** controla o espaço dentro de cada cartão.
    
- **Spacing:** controla o espaço entre os cartões.
    

## 17. 🧱 Código dos seis Borders

Uma reconstrução da estrutura mostrada na aula:

XML

```
<HorizontalStackLayout
    HorizontalOptions="Center"
    Spacing="5">

    <Border
        Stroke="#00AB37"
        StrokeShape="RoundRectangle 8"
        Padding="10,5">

        <Label
            Text="01"
            FontSize="24"
            FontFamily="OpenSansMedium"
            TextColor="#00AB37" />

    </Border>

    <Border
        Stroke="#00AB37"
        StrokeShape="RoundRectangle 8"
        Padding="10,5">

        <Label
            Text="05"
            FontSize="24"
            FontFamily="OpenSansMedium"
            TextColor="#00AB37" />

    </Border>

    <Border
        Stroke="#00AB37"
        StrokeShape="RoundRectangle 8"
        Padding="10,5">

        <Label
            Text="12"
            FontSize="24"
            FontFamily="OpenSansMedium"
            TextColor="#00AB37" />

    </Border>

    <Border
        Stroke="#00AB37"
        StrokeShape="RoundRectangle 8"
        Padding="10,5">

        <Label
            Text="18"
            FontSize="24"
            FontFamily="OpenSansMedium"
            TextColor="#00AB37" />

    </Border>

    <Border
        Stroke="#00AB37"
        StrokeShape="RoundRectangle 8"
        Padding="10,5">

        <Label
            Text="32"
            FontSize="24"
            FontFamily="OpenSansMedium"
            TextColor="#00AB37" />

    </Border>

    <Border
        Stroke="#00AB37"
        StrokeShape="RoundRectangle 8"
        Padding="10,5">

        <Label
            Text="47"
            FontSize="24"
            FontFamily="OpenSansMedium"
            TextColor="#00AB37" />

    </Border>

</HorizontalStackLayout>
```

> **Observação:** assim como na aula anterior, a transcrição contém ajustes feitos visualmente pelo professor e nem todos os valores finais aparecem de forma inequívoca. O código acima consolida a estrutura e os valores demonstrados, especialmente `#00AB37`, `Padding`, `RoundRectangle` e `Spacing`.

## 18. 🧠 Tabela completa dos conceitos

|**Conceito**|**Código**|**Função**|
|---|---|---|
|`Border`|`<Border>`|Cria uma borda ao redor do conteúdo|
|`Stroke`|`Stroke="#00AB37"`|Define a cor da borda|
|`StrokeShape`|`StrokeShape="RoundRectangle 8"`|Define o formato da borda|
|`RoundRectangle`|`RoundRectangle`|Retângulo com cantos arredondados|
|`Padding`|`Padding="10,5"`|Espaço interno|
|`Spacing`|`Spacing="5"`|Espaço entre elementos|
|`FontSize`|`FontSize="24"`|Tamanho do texto|
|`FontFamily`|`FontFamily="OpenSansMedium"`|Fonte utilizada|
|`TextColor`|`TextColor="#00AB37"`|Cor do texto|
|`HorizontalOptions`|`HorizontalOptions="Center"`|Centralização horizontal|

## 19. 🧠 Border × Label

É importante entender que eles têm responsabilidades diferentes:

XML

```
<Border>
    <Label Text="01" />
</Border>
```

- **Border:** Responsável pela caixa (`╭─────────╮ │ │ ╰─────────╯`)
    
- **Label:** Responsável pelo conteúdo (`01`)
    
- **Juntos:** (`╭─────────╮ │ 01 │ ╰─────────╯`)
    

## 20. 🎨 Propriedades visuais do número

A aparência final do número é resultado da combinação de várias propriedades:

XML

```
<Border
    Stroke="#00AB37"
    StrokeShape="RoundRectangle 8"
    Padding="10,5">

    <Label
        Text="01"
        FontSize="24"
        FontFamily="OpenSansMedium"
        TextColor="#00AB37" />

</Border>
```

Podemos separar:

Plaintext

```
BORDER
├── Stroke (cor)
├── StrokeShape (formato)
└── Padding (espaço interno)

LABEL
├── Text (número)
├── FontSize (tamanho)
├── FontFamily (fonte)
└── TextColor (cor)
```

## 21. 🔄 O que muda na próxima aula?

O professor termina dizendo que o layout está pronto. Até agora os números são estáticos (`01`, `05`, `12`...). Mas a proposta real do aplicativo é gerar números aleatórios.

Portanto, a próxima etapa será sair de:

Plaintext

```
XAML → números fixos
```

para:

Plaintext

```
C# → geração aleatória → atualização da interface → números da sorte
```

Além disso, ele menciona que posteriormente será implementada a transição entre as telas/estados da aplicação.

## 22. 🗺️ Mapa mental da aula

Plaintext

```
BORDER
│
├── Criar borda
│   └── <Border>
│
├── Cor
│   └── Stroke
│
├── Espaço interno
│   └── Padding
│
├── Formato
│   └── StrokeShape
│
├── Cantos arredondados
│   └── RoundRectangle
│
├── Conteúdo
│   └── Label
│
├── Repetição
│   └── 6 Borders
│
└── Organização
    └── HorizontalStackLayout
        │
        └── Spacing
```

## 23. 🎯 O que memorizar para revisão

Se você quiser transformar essa aula em poucas informações para revisar depois, guarde principalmente:

1. **Criar uma borda:**
    
    XML
    
    ```
    <Border>
        <Label Text="01" />
    </Border>
    ```
    
2. **Alterar a cor:** `Stroke="#00AB37"`
    
3. **Criar espaço interno:** `Padding="10,5"`
    
4. **Arredondar os cantos:** `StrokeShape="RoundRectangle 8"`
    
5. **Separar os números:** `Spacing="5"`
    
6. **Estrutura final:**
    
    XML
    
    ```
    <HorizontalStackLayout
        HorizontalOptions="Center"
        Spacing="5">
    
        <Border
            Stroke="#00AB37"
            StrokeShape="RoundRectangle 8"
            Padding="10,5">
    
            <Label
                Text="01"
                FontSize="24"
                TextColor="#00AB37" />
    
        </Border>
    
    </HorizontalStackLayout>
    ```
    

## 🎯 Essência da aula

O professor transforma cada número em um componente visual independente, usando `Border` como contêiner da `Label`. A `Border` define a aparência da caixa (`Stroke`, `StrokeShape`), enquanto a `Label` define o número e sua aparência (`Text`, `FontSize`, `TextColor`). O `Spacing` controla a distância entre as seis caixas. A próxima etapa será substituir os números fixos pela geração dinâmica em C#.