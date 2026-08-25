# .NET MAUI — Estilização do Menu do MAUI Gallery

## 1. Objetivo da aula

Depois de criar o menu dinamicamente, a interface ainda estava visualmente simples.

O objetivo desta aula é melhorar sua aparência, aplicando:

- Fonte;
    
- Tamanho da fonte;
    
- Negrito;
    
- Margens;
    
- Espaçamento entre elementos;
    
- Recuo dos componentes;
    
- Cor de fundo.
    

A ideia é aproximar o menu do design planejado para o **MAUI Gallery**.

---

# 2. Situação inicial

O menu já conseguia apresentar:

```text
Início
Extra
Créditos

Layouts

StackLayout
Organização sequencial dos elementos.
```

Porém, os elementos estavam muito próximos e sem uma diferenciação visual clara.

A nova estrutura será aproximadamente:

```text
MAUI Gallery

Início
Extra
Créditos

Layouts

    StackLayout
    Organização sequencial dos elementos.
```

Com diferentes tamanhos, pesos de fonte e espaçamentos.

---

# 3. Configuração do título

O título do aplicativo foi alterado para:

```text
MAUI Gallery
```

O `".NET"` foi removido para deixar a identidade visual mais simples.

Também foram aplicadas algumas propriedades:

```xml
<Label
    Text="MAUI Gallery"
    Margin="30"
    FontSize="24"
    FontFamily="OpenSans-SemiBold" />
```

### Principais propriedades

|Propriedade|Exemplo|Função|
|---|---|---|
|`Text`|`MAUI Gallery`|Texto exibido|
|`Margin`|`30`|Espaçamento externo|
|`FontSize`|`24`|Tamanho da fonte|
|`FontFamily`|`OpenSans-SemiBold`|Fonte utilizada|

---

# 4. Fontes disponíveis no projeto

O projeto .NET MAUI já possui algumas fontes configuradas.

Na aula foram utilizadas principalmente:

```text
OpenSans-Regular
OpenSans-SemiBold
```

A diferença básica é:

|Fonte|Característica|
|---|---|
|`OpenSans-Regular`|Peso normal|
|`OpenSans-SemiBold`|Mais espessa, próxima do negrito|

A fonte `SemiBold` foi utilizada para destacar títulos e categorias.

---

# 5. Configuração das fontes no `MauiProgram`

As fontes são registradas no `MauiProgram.cs`.

Conceitualmente:

```csharp
fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
fonts.AddFont("OpenSans-Semibold.ttf", "OpenSansSemiBold");
```

O segundo valor funciona como um **apelido** utilizado dentro do aplicativo.

Por exemplo:

```xml
FontFamily="OpenSansSemiBold"
```

Assim, o XAML não precisa utilizar diretamente o nome completo do arquivo da fonte.

---

# 6. `FontFamily`

A propriedade:

```text
FontFamily
```

define qual fonte será utilizada pelo elemento.

Exemplo:

```xml
<Label
    Text="MAUI Gallery"
    FontFamily="OpenSansSemiBold" />
```

No C#:

```csharp
label.FontFamily = "OpenSansSemiBold";
```

Portanto, a mesma propriedade pode ser utilizada tanto no XAML quanto no C#.

---

# 7. XAML e C# utilizam as mesmas propriedades

Um dos conceitos importantes apresentados é que os elementos criados pelo C# possuem as mesmas propriedades disponíveis nos elementos definidos pelo XAML.

### XAML

```xml
<Label
    FontFamily="OpenSansSemiBold"
    FontSize="24" />
```

### C#

```csharp
label.FontFamily = "OpenSansSemiBold";
label.FontSize = 24;
```

Isso acontece porque, nos dois casos, estamos trabalhando com objetos do .NET MAUI.

---

# 8. `Margin`

A propriedade `Margin` cria um espaço **externo** ao elemento.

Exemplo:

```xml
<Label
    Margin="20" />
```

Isso cria uma distância de `20` em todos os lados:

```text
        20
   ┌───────────┐
20 │   Label   │ 20
   └───────────┘
        20
```

Portanto:

```text
Margin="20"
```

equivale conceitualmente a:

```text
Esquerda = 20
Superior = 20
Direita = 20
Inferior = 20
```

---

# 9. Margens individuais

Também é possível definir valores diferentes para cada lado.

A ordem utilizada é:

```text
Esquerda, Superior, Direita, Inferior
```

Exemplo:

```xml
Margin="20,10,0,0"
```

Significa:

|Posição|Valor|
|---|--:|
|Esquerda|20|
|Superior|10|
|Direita|0|
|Inferior|0|

Representação:

```text
Margin="Left, Top, Right, Bottom"
```

---

# 10. `Padding` x `Margin`

É importante diferenciar os dois conceitos.

### `Margin`

Cria espaço **fora** do elemento.

```text
        Margin
          ↓
   ┌───────────────┐
   │   Elemento    │
   └───────────────┘
```

### `Padding`

Cria espaço **dentro** do elemento.

```text
┌───────────────────────┐
│   Padding             │
│     ┌─────────────┐   │
│     │  Conteúdo   │   │
│     └─────────────┘   │
└───────────────────────┘
```

Resumo:

|Propriedade|Espaço|
|---|---|
|`Margin`|Externo|
|`Padding`|Interno|

---

# 11. Espaçamento entre elementos com `Spacing`

O `VerticalStackLayout` possui a propriedade:

```xml
Spacing="10"
```

Ela cria uma distância entre os elementos filhos.

Exemplo:

```xml
<VerticalStackLayout
    Spacing="10">
    
    <Label Text="Início" />
    <Label Text="Extra" />
    <Label Text="Créditos" />

</VerticalStackLayout>
```

Resultado conceitual:

```text
Início
   ↓ 10
Extra
   ↓ 10
Créditos
```

---

# 12. Diferença entre `Spacing` e `Margin`

Embora ambos criem espaços, eles funcionam de maneiras diferentes.

|Recurso|Função|
|---|---|
|`Spacing`|Cria espaço entre os filhos de um `StackLayout`|
|`Margin`|Cria espaço externo individual de um elemento|

Exemplo:

```text
VerticalStackLayout
│
├── Label
│
│  ← Spacing
│
├── Label
│
│  ← Spacing
│
└── Label
```

Já a margem pertence individualmente ao elemento:

```text
Label
└── Margin
```

---

# 13. Aplicando estilo às categorias

As categorias também serão destacadas visualmente.

No código C#, a `Label` que representa a categoria pode receber:

```csharp
lblCategory.FontFamily = "OpenSansSemiBold";
```

Assim:

```text
Layouts
```

fica visualmente diferente dos componentes.

A categoria passa a funcionar como um **título de seção**.

---

# 14. Aplicando estilo ao título do componente

O título do componente também recebe a fonte `SemiBold`.

Exemplo:

```csharp
lblComponentTitle.FontFamily = "OpenSansSemiBold";
```

Assim:

```text
Layouts

StackLayout
Organização sequencial dos elementos.
```

O `StackLayout` recebe maior destaque que sua descrição.

---

# 15. Criando recuo dos componentes

Os componentes pertencentes a uma categoria precisam apresentar um recuo para deixar clara a hierarquia.

Foi aplicada uma margem ao título:

```csharp
lblComponentTitle.Margin = new Thickness(20, 10, 0, 0);
```

E também à descrição:

```csharp
lblComponentDescription.Margin = new Thickness(20, 10, 0, 0);
```

A ideia visual é:

```text
Layouts
   │
   ├── StackLayout
   │
   └── Organização sequencial dos elementos.
```

O `20` no primeiro valor cria o recuo à esquerda.

---

# 16. Classe `Thickness`

A propriedade `Margin` utiliza a estrutura:

```text
Thickness
```

Exemplo:

```csharp
new Thickness(20, 10, 0, 0)
```

A ordem é:

```text
new Thickness(
    esquerda,
    superior,
    direita,
    inferior
)
```

Portanto:

```csharp
new Thickness(20, 10, 0, 0)
```

significa:

```text
Left   = 20
Top    = 10
Right  = 0
Bottom = 0
```

---

# 17. Ajustando o espaço entre título e descrição

Inicialmente, o mesmo `Margin` foi aplicado aos dois elementos.

Porém, isso deixava o título e a descrição muito afastados.

A solução foi reduzir a margem superior da descrição:

```csharp
lblComponentDescription.Margin =
    new Thickness(20, 0, 0, 0);
```

Assim:

```text
StackLayout
Descrição do StackLayout.
```

ficam mais próximos.

---

# 18. Cor de fundo

Também foi alterada a cor de fundo do menu.

A cor utilizada foi:

```text
#F3F3F3
```

Exemplo:

```xml
BackgroundColor="#F3F3F3"
```

Isso proporciona um fundo cinza claro.

Visualmente:

```text
┌─────────────────────────────┐
│ MAUI Gallery                │
│                             │
│ Início                      │
│ Extra                       │
│ Créditos                    │
│                             │
│ Layouts                     │
│     StackLayout             │
│     Descrição...            │
└─────────────────────────────┘
```

---

# 19. Resultado visual

Depois das alterações, o menu passa a ter uma hierarquia visual mais clara:

```text
MAUI Gallery

Início
Extra
Créditos

Layouts

    StackLayout
    Organização sequencial dos elementos.
```

Onde:

- `MAUI Gallery` → título principal;
    
- `Início`, `Extra` e `Créditos` → opções principais;
    
- `Layouts` → categoria;
    
- `StackLayout` → componente;
    
- descrição → informação complementar.
    

---

# 20. Hierarquia visual

A estilização ajuda a representar a hierarquia dos dados:

```text
MAUI Gallery
      ↓
Menu
      ↓
Categoria
      ↓
Componente
      ↓
Descrição
```

Visualmente:

```text
MAUI Gallery        ← maior destaque

Início
Extra
Créditos

Layouts             ← categoria

    StackLayout     ← componente
    Descrição       ← informação
```

---

# 21. Alterações feitas no XAML

No XAML, foram utilizadas propriedades como:

```xml
<Label
    Text="MAUI Gallery"
    Margin="30"
    FontSize="24"
    FontFamily="OpenSansSemiBold" />
```

E no `VerticalStackLayout`:

```xml
<VerticalStackLayout
    x:Name="MenuContainer"
    Padding="20"
    Spacing="10"
    BackgroundColor="#F3F3F3">
```

Essas propriedades ajudam a controlar:

- posicionamento;
    
- espaçamento;
    
- tamanho;
    
- fonte;
    
- cor;
    
- organização dos elementos.
    

---

# 22. Alterações feitas no C#

Como os componentes de categoria e título são criados dinamicamente, suas propriedades precisam ser configuradas pelo C#.

Exemplo:

```csharp
var lblCategory = new Label
{
    Text = category.Name,
    FontFamily = "OpenSansSemiBold"
};
```

E:

```csharp
var lblComponentTitle = new Label
{
    Text = component.Title,
    FontFamily = "OpenSansSemiBold",
    Margin = new Thickness(20, 10, 0, 0)
};
```

Descrição:

```csharp
var lblComponentDescription = new Label
{
    Text = component.Description,
    Margin = new Thickness(20, 0, 0, 0)
};
```

---

# 23. Reinicialização do aplicativo

Uma observação importante da aula é que algumas alterações feitas diretamente no C# não aparecem imediatamente durante a execução.

Por isso, pode ser necessário:

```text
Alterar código
     ↓
Parar aplicativo
     ↓
Executar novamente
     ↓
Ver alteração
```

Enquanto algumas alterações feitas no XAML podem ser visualizadas mais rapidamente dependendo do ambiente e do Hot Reload.

---

# 24. Resumo dos principais conceitos

|Conceito|Função|
|---|---|
|`FontFamily`|Define a família da fonte|
|`FontSize`|Define o tamanho do texto|
|`Margin`|Cria espaço externo|
|`Padding`|Cria espaço interno|
|`Spacing`|Cria espaço entre filhos de um `StackLayout`|
|`Thickness`|Estrutura utilizada para definir valores de margem/padding|
|`FontWeight`/fonte `SemiBold`|Aumenta o destaque visual do texto|
|`BackgroundColor`|Define a cor de fundo|
|`x:Name`|Permite acessar um elemento XAML pelo C#|
|`Children`|Coleção de elementos filhos|
|`FontFamily` no C#|Permite alterar a fonte de elementos criados dinamicamente|

---

# 25. `Margin` — para memorizar

A ordem:

```text
Left, Top, Right, Bottom
```

Exemplo:

```csharp
new Thickness(20, 10, 0, 0);
```

Significa:

```text
Esquerda = 20
Superior = 10
Direita  = 0
Inferior = 0
```

---

# 26. Comparação rápida

|Propriedade|Exemplo|O que controla|
|---|---|---|
|`FontSize`|`24`|Tamanho do texto|
|`FontFamily`|`"OpenSansSemiBold"`|Fonte|
|`Margin`|`20`|Espaço externo|
|`Padding`|`20`|Espaço interno|
|`Spacing`|`10`|Espaço entre filhos|
|`BackgroundColor`|`#F3F3F3`|Cor de fundo|
|`Text`|`"Layouts"`|Conteúdo textual|

---

# 27. Estrutura final da estilização

```text
VerticalStackLayout
│
├── Padding = 20
├── Spacing = 10
├── BackgroundColor = #F3F3F3
│
├── MAUI Gallery
│   ├── FontSize = 24
│   ├── FontFamily = SemiBold
│   └── Margin = 30
│
├── Início
├── Extra
├── Créditos
│
├── Layouts
│   └── FontFamily = SemiBold
│
├── StackLayout
│   ├── FontFamily = SemiBold
│   └── Margin = 20,10,0,0
│
└── Descrição
    └── Margin = 20,0,0,0
```

---

# 28. Ideia principal da aula

A principal lição é que **as propriedades visuais dos componentes do MAUI podem ser configuradas tanto no XAML quanto no C#**.

Por exemplo:

```xml
FontFamily="OpenSansSemiBold"
```

é equivalente a:

```csharp
label.FontFamily = "OpenSansSemiBold";
```

E:

```xml
Margin="20"
```

é equivalente conceitualmente a:

```csharp
label.Margin = new Thickness(20);
```

Isso é especialmente importante neste projeto porque o menu está sendo criado **dinamicamente pelo C#**.

A estrutura agora é:

```text
Repository
    ↓
Category
    ↓
Component
    ↓
C# cria Label
    ↓
C# configura aparência
    ↓
Children.Add()
    ↓
Menu estilizado
```

**Próxima etapa:** adicionar comportamento aos elementos do menu, permitindo que o usuário clique em um componente, como `StackLayout`, e seja direcionado para a página de demonstração correspondente.