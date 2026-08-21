# .NET MAUI — Controle de Estados, Visibilidade e Eventos

## 1. 🎯 Objetivo da aula

A tela possui, basicamente, dois estados:

|Estado|Label "Número da sorte"|Container com números|
|---|---|---|
|**Inicial**|👁️ Visível|🚫 Invisível|
|**Após clicar**|🚫 Invisível|👁️ Visível|

**Visualmente:**

**ESTADO INICIAL**

```
┌─────────────────────┐
│   Número da sorte   │
│                     │
│   [ Gerar ]         │
└─────────────────────┘
```

**Depois do clique:**

**ESTADO FINAL**

```
┌─────────────────────┐
│  15   42   07       │
│  23   38   51       │
│                     │
│   Boa sorte!        │
└─────────────────────┘
```

Neste momento da aula, o professor ainda não implementa o sorteio dos números. Ele apenas implementa a troca visual entre os dois estados.

## 2. 👥 Criando um "grupo" de elementos

Um dos primeiros problemas é: **Como esconder vários elementos de uma vez?**

Imagine que temos:



```XML
<Label Text="01" />
<Label Text="02" />
<Label Text="03" />
<Label Text="04" />
<Label Text="05" />
<Label Text="06" />
```

Seria possível fazer:



```C#
label01.IsVisible = false;
label02.IsVisible = false;
label03.IsVisible = false;
label04.IsVisible = false;
label05.IsVisible = false;
label06.IsVisible = false;
```

Mas isso é trabalhoso. A solução apresentada é colocar os elementos dentro de um container.

## 3. 📦 VerticalStackLayout como container

O .NET MAUI não possui necessariamente um componente chamado simplesmente "Group" para agrupar elementos visualmente. Então podemos usar um `VerticalStackLayout`:



```XML
<VerticalStackLayout>
    ...
</VerticalStackLayout>
```

Ele passa a funcionar como um container. Por exemplo:



```XML
<VerticalStackLayout>
    <Label Text="01" />
    <Label Text="02" />
    <Label Text="03" />
</VerticalStackLayout>
```

Agora, em vez de controlar três Labels individualmente, podemos controlar apenas o `VerticalStackLayout`:



```C#
container.IsVisible = false;
```

Isso esconde todos os elementos que estão dentro dele.

> **Ideia fundamental:**
> 
> VerticalStackLayout
> 
> ├── Label 01
> 
> ├── Label 02
> 
> └── Label 03
> 
> Se `VerticalStackLayout.IsVisible = false;`, todo o conteúdo fica invisível.

## 4. ⚠️ Um detalhe sobre performance

O professor chama atenção para uma questão importante. Criar um container significa adicionar mais um elemento à árvore visual:


```
ContentPage
   │
   └── VerticalStackLayout
          │
          ├── Label
          ├── Label
          └── Label
```

Esse `VerticalStackLayout` é mais um objeto/componente que precisa ser criado e gerenciado.

- Agrupar elementos dessa maneira tem um pequeno custo.
    
- Em uma aplicação pequena, isso não representa um problema relevante:
    
    - Poucos elementos → Poucos componentes → Impacto praticamente irrelevante
        
- Em interfaces muito grandes, criar muitos containers desnecessariamente pode aumentar a complexidade da árvore visual e afetar desempenho.
    

## 5. 🧠 MVVM

O professor também comenta que futuramente será apresentado o padrão **MVVM** (_Model – View – ViewModel_).

Neste momento, porém, o objetivo é ensinar a lógica diretamente no **Code Behind**:

XAML (Interface)→Code Behind (Manipulac¸​a˜o dos elementos)

Mais adiante, com MVVM, seria possível separar melhor:

View→ViewModel→Estado da aplicac¸​a˜o

Por enquanto, a solução mais simples é suficiente.

## 6. 👁️ A propriedade IsVisible

A propriedade fundamental da aula é `IsVisible`. Ela determina se um elemento deve ser visualizado:

|Valor|Resultado|
|---|---|
|`true`|👁️ Elemento visível|
|`false`|🚫 Elemento invisível|

**Exemplo:**



```XML
<Label
    Text="Número da sorte"
    IsVisible="True" />
```

_A Label aparece._



```XML
<VerticalStackLayout
    IsVisible="False">
    ...
</VerticalStackLayout>
```

_O container e seu conteúdo não aparecem._

## 7. 🏁 Definindo o estado inicial

A tela começa assim:

- **Label "Número da sorte":** `IsVisible = true`
    
- **Container dos números:** `IsVisible = false`
    

**Em XAML:**



```XML
<Label
    Text="Número da sorte"
    IsVisible="True" />

<VerticalStackLayout
    IsVisible="False">
    ...
</VerticalStackLayout>
```

**Portanto:**

- **Inicial:**
    
    - Label → `TRUE`
        
    - Container → `FALSE`
        

## 8. 🏷️ Dando nomes aos elementos com x:Name

Para que o C# encontre os elementos do XAML, precisamos dar um nome a eles usando `x:Name`:



```XML
<Label
    x:Name="lblLucky"
    Text="Número da sorte" />
```

Agora podemos acessar esse elemento diretamente no C#: `lblLucky`.

## 9. 🔗 O que x:Name faz?

`x:Name="lblLucky"` cria uma referência que permite ao Code Behind acessar aquele elemento.

```
XAML (x:Name="lblLucky") ───► Code Behind (lblLucky)
```

Isso permite fazer:



```C#
lblLucky.IsVisible = false;
```

## 10. 📦 Nomeando o container

Da mesma forma, o container recebe um nome:



```XML
<VerticalStackLayout
    x:Name="containerLuckyNumbers"
    IsVisible="False">
```

Agora podemos controlar o container no C#:



```C#
containerLuckyNumbers.IsVisible = true;
```

Temos então duas referências:

- `lblLucky` → Label "Número da sorte"
    
- `containerLuckyNumbers` → Container dos números
    

## 11. 🔢 Nomeando os números

O professor também precisa alterar os números posteriormente. Por isso, cada Label recebe um nome:



```XML
<Label x:Name="lblNumber01" />
<Label x:Name="lblNumber02" />
<Label x:Name="lblNumber03" />
<Label x:Name="lblNumber04" />
<Label x:Name="lblNumber05" />
<Label x:Name="lblNumber06" />
```

A ideia é posteriormente poder fazer:



```C#
lblNumber01.Text = "15";
lblNumber02.Text = "23";
lblNumber03.Text = "07";
```

## 12. 🧹 Os textos podem começar vazios

Como os números serão gerados pelo código, não precisamos deixar valores fixos no XAML.

Podemos ter:



```XML
<Label x:Name="lblNumber01" />
```

em vez de:



```XML
<Label
    x:Name="lblNumber01"
    Text="01" />
```

Posteriormente:



```C#
lblNumber01.Text = "15";
```

**Separação de responsabilidades:**

|Responsabilidade|Local|
|---|---|
|Estrutura da interface|XAML|
|Número sorteado|C#|
|Alteração do texto|C#|
|Controle de visibilidade|C#|

## 13. 💻 Code Behind

Depois de preparar o XAML, o professor passa para o Code Behind (arquivo `.xaml.cs` associado à tela XAML):

MainPage.xaml (Interface)⟷MainPage.xaml.cs (Comportamento / Programac¸​a˜o)

- O XAML define **como a tela é**.
    
- O C# define **como a tela se comporta**.
    

## 14. 🛠️ Criando o método

O professor cria:



```C#
private void OnGenerateLuckyNumbers()
{
    
}
```

|Parte|Significado|
|---|---|
|`private`|Só pode ser acessado dentro da classe|
|`void`|Não retorna um valor|
|`OnGenerateLuckyNumbers`|Nome do método|
|`()`|Sem parâmetros|

O método representa a ação: _"Gerar os números da sorte"_. Embora, neste momento, ele apenas troque a interface sem gerar números.

## 15. 🔄 Alterando IsVisible pelo C#

- **Esconda a Label:** `lblLucky.IsVisible = false;`
    
- **Mostre o container:** `containerLuckyNumbers.IsVisible = true;`
    

C#

```
private void OnGenerateLuckyNumbers()
{
    lblLucky.IsVisible = false;
    containerLuckyNumbers.IsVisible = true;
}
```

Essa é a essência da primeira parte da programação.

## 16. 🔍 Por que o C# consegue acessar o XAML?

Não estamos simplesmente manipulando uma "tag XML". A Label representa um objeto/classe:

- **Label:**
    
    - `Text`
        
    - `FontSize`
        
    - `FontFamily`
        
    - `IsVisible`
        
    - `Margin`
        
    - `Padding`
        
    - _Outras propriedades..._
        

Portanto, `lblLucky.IsVisible` está acessando uma propriedade de um objeto instanciado.

## 17. 🧩 Label é uma classe

Quando escrevemos `<Label/>`, temos a instância de uma classe `Label`. Por isso podemos acessar:

- `lblLucky.Text`
    
- `lblLucky.FontSize`
    
- `lblLucky.IsVisible`
    
- `lblLucky.Margin`
    

## 18. 🖱️ Ligando o método ao botão

O método precisa ser executado quando o usuário clicar no botão através do evento `Clicked`:



```XML
<Button
    Text="Gerar"
    Clicked="OnGenerateLuckyNumbers" />
```

**Fluxo:**

Usuaˊrio clica→Button (Clicked)→OnGenerateLuckyNumbers()

## 19. ⚡ Eventos no .NET MAUI

> **Conceito:** Evento é uma forma de avisar que alguma coisa aconteceu.

|Evento|Acontecimento|
|---|---|
|`Clicked`|Usuário clicou|
|`TextChanged`|Texto mudou|
|`CheckedChanged`|Checkbox mudou|
|`SelectedIndexChanged`|Seleção mudou|

## 20. 📡 O sender

O método disparado por eventos normalmente possui:



```C#
private void Button_Clicked(object sender, EventArgs e)
{
    
}
```

O parâmetro `object sender` representa **quem disparou o evento** (neste caso, o botão clicado).

## 21. 🔄 Casting do sender

Como `sender` é declarado genericamente como `object`, fazemos um casting para tratá-lo como `Button` e acessar suas propriedades específicas:



```C#
Button button = (Button)sender;
button.Text = "Gerado!";
```

## 22. 📦 O parâmetro EventArgs

O segundo parâmetro, `EventArgs e`, representa os argumentos associados ao evento.

- No `Clicked`, `EventArgs` contém poucas informações específicas.
    
- Em outros eventos (como mouse/toque), fornece detalhes como posição X, posição Y, tipo de interação, etc.
    

## 23. 🧠 O "ecossistema" dos eventos


```C#

private void Button_Clicked(
    object sender,
    EventArgs e)
{
    // código
}
```

- `sender` → Responde: _Quem disparou o evento?_
    
- `e` → Responde: _Quais informações acompanham esse evento?_
    

## 24. 🔗 A ligação final

Plaintext

```
                    XAML
                     │
          ┌──────────┴──────────┐
          │                     │
       Button                Elements
          │                     │
       Clicked             x:Name
          │                     │
          ↓                     ↓
 OnGenerateLuckyNumbers()      C#
          │
          ├── lblLucky
          │      └── IsVisible = false
          │
          └── containerLuckyNumbers
                 └── IsVisible = true
```

## 25. 🧪 O que acontece quando executamos?

- **Antes do clique:**
    
    - `lblLucky.IsVisible = true`
        
    - `containerLuckyNumbers.IsVisible = false`
        
    - **Tela:** Label visível e botão `[ GERAR ]`.
        
- **Usuário clica:**
    
    - O evento `Clicked` é disparado → Executa `OnGenerateLuckyNumbers();`
        
    - `lblLucky.IsVisible = false;`
        
    - `containerLuckyNumbers.IsVisible = true;`
        
    - **Resultado:** O container com os números e a mensagem "Boa sorte!" aparecem.
        

## 26. 🔁 Por que o segundo clique não muda nada?

Depois do primeiro clique, as propriedades já estão configuradas como `lblLucky.IsVisible = false` e `containerLuckyNumbers.IsVisible = true`.

Ao clicar novamente, o código apenas reatribui os mesmos valores para o estado em que a interface já se encontra. O algoritmo de geração dos números da sorte será implementado na aula seguinte.

## 27. 📚 Resumo dos conceitos da aula

| Conceito              | O que significa                        | Exemplo                    |
| --------------------- | -------------------------------------- | -------------------------- |
| `VerticalStackLayout` | Container para agrupar elementos       | `<VerticalStackLayout>`    |
| `IsVisible`           | Controla visibilidade                  | `IsVisible="False"`        |
| `x:Name`              | Dá um nome ao elemento                 | `x:Name="lblLucky"`        |
| Code Behind           | C# associado à tela XAML               | `MainPage.xaml.cs`         |
| Método                | Bloco de código executável             | `OnGenerateLuckyNumbers()` |
| `Clicked`             | Evento disparado pelo clique           | `Clicked="..."`            |
| `sender`              | Objeto que disparou o evento           | `Button`                   |
| `EventArgs`           | Informações do evento                  | `EventArgs e`              |
| Casting               | Conversão para um tipo específico      | `(Button)sender`           |
| Propriedade           | Característica do objeto               | `IsVisible`, `Text`        |
| MVVM                  | Padrão para separar interface e lógica | `View` + `ViewModel`       |

## 28. 🧠 O conhecimento mais importante para a prova/prática

Plaintext

```
1. Tenho vários elementos
   ↓
2. Coloco-os em um container
   ↓
3. Dou um x:Name ao container
   ↓
4. Uso IsVisible para controlar sua exibição
   ↓
5. Dou x:Name aos elementos que preciso controlar
   ↓
6. Acesso esses elementos pelo Code Behind
   ↓
7. Manipulo suas propriedades
   ↓
8. Ligo um método a um evento
   ↓
9. O evento dispara o método
```

### Exemplo mínimo

**XAML:**

```XML
<Label
    x:Name="lblLucky"
    Text="Número da sorte"
    IsVisible="True" />

<VerticalStackLayout
    x:Name="containerLuckyNumbers"
    IsVisible="False">

    <Label x:Name="lblNumber01" />
    <Label x:Name="lblNumber02" />
    <Label x:Name="lblNumber03" />

</VerticalStackLayout>

<Button
    Text="Gerar"
    Clicked="OnGenerateLuckyNumbers" />
```

**Code Behind:**

```C#
private void OnGenerateLuckyNumbers(
    object sender,
    EventArgs e)
{
    lblLucky.IsVisible = false;
    containerLuckyNumbers.IsVisible = true;
}
```