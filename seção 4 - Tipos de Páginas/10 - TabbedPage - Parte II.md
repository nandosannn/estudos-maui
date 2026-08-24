# Customização visual da TabbedPage no .NET MAUI

## 1. Objetivo da aula

Nesta aula aprendemos como personalizar visualmente o sistema de abas da `TabbedPage`.

As principais propriedades apresentadas são:

```text
BarBackground
BarBackgroundColor
SelectedTabColor
UnselectedTabColor
BarTextColor
```

Essas propriedades permitem alterar:

- cor do fundo da barra de abas;
    
- cor da aba selecionada;
    
- cor das abas não selecionadas;
    
- cor dos textos das abas;
    
- preenchimento utilizando cores ou `Brush`.
    

---

# 2. Diferenças entre as plataformas

Um dos pontos mais importantes da aula é entender que o .NET MAUI é multiplataforma.

A mesma propriedade pode produzir resultados diferentes em:

- Windows;
    
- Android;
    
- iOS;
    
- macOS.
    

Isso acontece porque o .NET MAUI utiliza componentes e recursos nativos de cada sistema operacional.

Podemos representar:

```text
.NET MAUI
    │
    ├── Windows
    │
    ├── Android
    │
    ├── iOS
    │
    └── macOS
```

Por isso, uma configuração visual que funciona muito bem no Windows pode apresentar um resultado diferente no Android ou no iOS.

---

# 3. Por que testar em cada plataforma?

Ao criar uma interface multiplataforma, não devemos assumir que:

```text
Uma configuração no Windows
        =
A mesma aparência no Android
        =
A mesma aparência no iOS
```

Na prática:

```text
Windows → comportamento A
Android → comportamento B
iOS     → comportamento C
```

Portanto, é importante testar a interface nos dispositivos que o aplicativo pretende atender.

---

# 4. Sistema de abas no Windows

No Windows, a `TabbedPage` apresenta as abas com um determinado estilo visual.

Existe um indicador que mostra qual aba está atualmente selecionada.

Por exemplo:

```text
+------------------------------------------------+
| Página 1 | Página 2 | Página 3                 |
+------------------------------------------------+
|__________                                        |
```

O indicador muda de posição quando o usuário troca de aba.

Se selecionarmos a Página 2:

```text
+------------------------------------------------+
| Página 1 | Página 2 | Página 3                 |
+------------------------------------------------+
             __________
```

Esse indicador ajuda o usuário a identificar qual página está ativa.

---

# 5. Propriedades de customização

A aula apresenta quatro elementos principais de personalização.

Podemos resumir:

|Propriedade|Função|
|---|---|
|`BarBackgroundColor`|Define uma cor sólida para o fundo da barra|
|`BarBackground`|Permite utilizar um `Brush` como fundo|
|`SelectedTabColor`|Define a aparência/cor relacionada à aba selecionada|
|`UnselectedTabColor`|Define a aparência/cor das abas não selecionadas|
|`BarTextColor`|Define a cor dos textos das abas|

Essas propriedades permitem modificar significativamente a aparência da `TabbedPage`.

---

# 6. BarBackgroundColor

A propriedade:

```xml
BarBackgroundColor
```

permite definir uma **cor sólida** para o fundo da barra de abas.

Exemplo:

```xml
<TabbedPage
    BarBackgroundColor="Blue">
```

O resultado seria aproximadamente:

```text
+------------------------------------------------+
| Página 1 | Página 2 | Página 3                 |
+------------------------------------------------+
|             fundo azul                        |
```

A ideia principal é:

```text
BarBackgroundColor
        ↓
Cor sólida
        ↓
Fundo da barra
```

---

# 7. Utilizando a classe Color

O `BarBackgroundColor` trabalha com a classe `Color` do .NET MAUI.

Podemos utilizar nomes de cores:

```xml
BarBackgroundColor="Blue"
```

```xml
BarBackgroundColor="Red"
```

```xml
BarBackgroundColor="Green"
```

```xml
BarBackgroundColor="White"
```

```xml
BarBackgroundColor="Black"
```

Também podemos utilizar valores hexadecimais.

Por exemplo:

```xml
BarBackgroundColor="#0000FF"
```

ou:

```xml
BarBackgroundColor="#FF0000"
```

Também podemos trabalhar com transparência utilizando o canal Alpha.

Por exemplo:

```xml
BarBackgroundColor="#800000FF"
```

Nesse caso, o valor hexadecimal possui informações relacionadas à transparência.

---

# 8. BarBackground

Outra propriedade apresentada é:

```xml
BarBackground
```

A diferença principal é que ela utiliza um `Brush`.

Enquanto:

```xml
BarBackgroundColor
```

trabalha com uma cor, o:

```xml
BarBackground
```

permite utilizar um preenchimento mais elaborado.

Podemos pensar:

```text
BarBackgroundColor
        ↓
Uma única cor

BarBackground
        ↓
Brush
        ↓
Possibilidades de preenchimento
```

---

# 9. O que é Brush?

A palavra `Brush` pode ser entendida literalmente como "pincel".

No contexto do .NET MAUI, um `Brush` representa uma forma de preencher uma área.

Ele permite criar efeitos mais elaborados do que simplesmente utilizar uma cor.

Por exemplo:

```text
Cor sólida
████████████████

Gradiente
██████▓▓▓▒▒▒░░░
```

---

# 10. Gradientes

Com `Brush`, podemos criar efeitos como gradientes.

Um gradiente representa uma transição entre duas ou mais cores.

Por exemplo:

```text
Azul → Roxo
██████▓▓▓▓▒▒▒▒░░
```

Podemos ter diferentes tipos de gradiente, como:

- linear;
    
- radial.
    

### Gradiente linear

A transição acontece seguindo uma direção.

```text
Cor A → Cor B
████████▓▓▓▓▒▒▒▒░░░░
```

### Gradiente radial

A transição ocorre a partir de um ponto central ou focal.

```text
      ███
    ███████
   █████████
    ▓▓▓▓▓▓▓
      ░░░
```

Portanto:

```text
Color
 ↓
Cor simples

Brush
 ↓
Preenchimento personalizado
 ↓
Gradientes e outros efeitos
```

---

# 11. SelectedTabColor

Outra propriedade apresentada é:

```xml
SelectedTabColor
```

Ela está relacionada à aparência da aba que está atualmente selecionada.

Por exemplo:

```xml
SelectedTabColor="Green"
```

Se a Página 3 estiver selecionada:

```text
+------------------------------------------------+
| Página 1 | Página 2 | Página 3                 |
|                       ████████                 |
+------------------------------------------------+
```

A aparência relacionada ao item selecionado será alterada conforme o comportamento da plataforma.

---

# 12. Comportamento diferente no Android

Um ponto muito importante da aula é que `SelectedTabColor` não necessariamente produz o mesmo resultado em todas as plataformas.

No Windows, a propriedade pode afetar o fundo ou o indicador da aba.

No Android, o comportamento pode ser diferente.

Por exemplo, a cor pode ser aplicada aos elementos relacionados à aba selecionada, como:

```text
Ícone
Texto
Indicador
```

Podemos representar:

```text
Windows
↓
Pode alterar o fundo/indicador

Android
↓
Pode alterar texto/ícone/indicador
```

Por isso, é fundamental testar a interface diretamente no Android.

---

# 13. UnselectedTabColor

A propriedade:

```xml
UnselectedTabColor
```

é utilizada para definir a aparência das abas que **não estão selecionadas**.

Por exemplo:

```xml
UnselectedTabColor="LightGray"
```

Se a Página 3 estiver selecionada:

```text
+------------------------------------------------+
| Página 1 | Página 2 | Página 3                 |
| Cinza    | Cinza    | Selecionada             |
+------------------------------------------------+
```

A Página 1 e a Página 2 são consideradas não selecionadas.

Portanto:

```text
SelectedTabColor
        ↓
Aba selecionada

UnselectedTabColor
        ↓
Abas não selecionadas
```

---

# 14. Exemplo de combinação

Podemos utilizar:

```xml
<TabbedPage
    BarBackgroundColor="White"
    SelectedTabColor="Green"
    UnselectedTabColor="LightGray">
```

A ideia seria:

```text
Barra
┌──────────────────────────────────────────────┐
│ Página 1 | Página 2 | Página 3               │
│  cinza      cinza       verde                │
└──────────────────────────────────────────────┘
```

O resultado exato dependerá da plataforma.

---

# 15. BarTextColor

A última propriedade apresentada é:

```xml
BarTextColor
```

Ela permite definir a cor do texto das abas.

Por exemplo:

```xml
BarTextColor="White"
```

Se anteriormente os textos eram pretos:

```text
Página 1 | Página 2 | Página 3
   ↓           ↓          ↓
  Preto       Preto      Preto
```

Depois:

```text
Página 1 | Página 2 | Página 3
   ↓           ↓          ↓
  Branco      Branco     Branco
```

---

# 16. Exemplo de customização completa

Podemos combinar as propriedades:

```xml
<TabbedPage
    BarBackgroundColor="Blue"
    SelectedTabColor="Yellow"
    UnselectedTabColor="LightGray"
    BarTextColor="White">
```

Temos:

```text
BarBackgroundColor
        ↓
Fundo azul

SelectedTabColor
        ↓
Aba selecionada em amarelo

UnselectedTabColor
        ↓
Abas não selecionadas em cinza

BarTextColor
        ↓
Textos em branco
```

---

# 17. Resumo visual das propriedades

```text
                 TabbedPage
                     │
        ┌────────────┼────────────┐
        │            │            │
        ↓            ↓            ↓
BarBackground   SelectedTab   UnselectedTab
     │              │              │
     ↓              ↓              ↓
 Fundo da        Aba ativa      Abas inativas
   barra
                     │
                     ↓
               BarTextColor
                     │
                     ↓
                Texto das abas
```

---

# 18. Diferença entre Color e Brush

Essa é uma distinção importante da aula.

|Recurso|Tipo|Utilização|
|---|---|---|
|`Color`|Cor|Uma cor específica|
|`Brush`|Preenchimento|Cores e efeitos mais elaborados|
|`BarBackgroundColor`|`Color`|Fundo com uma cor|
|`BarBackground`|`Brush`|Fundo com preenchimento personalizado|

Exemplo simples:

```xml
BarBackgroundColor="Blue"
```

Representa:

```text
████████████████████
```

Já um `Brush` pode permitir algo como:

```text
██████▓▓▓▓▒▒▒░░░░
```

ou um efeito radial.

---

# 19. Código resumido

Uma configuração básica pode ser:

```xml
<TabbedPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    BarBackgroundColor="Blue"
    SelectedTabColor="Yellow"
    UnselectedTabColor="LightGray"
    BarTextColor="White">

    <pages:Page1 />

    <pages:Page2 />

    <pages:Page3 />

</TabbedPage>
```

Essa configuração personaliza:

```text
Fundo da barra      → Azul
Aba selecionada     → Amarelo
Abas não selecionadas → Cinza claro
Texto                → Branco
```

O resultado visual poderá variar dependendo da plataforma.

---

# 20. Por que o resultado pode variar?

O .NET MAUI trabalha com uma abstração multiplataforma.

Isso significa que escrevemos:

```xml
SelectedTabColor="Green"
```

mas o sistema operacional precisa transformar essa configuração em um componente visual nativo.

Podemos representar:

```text
Código MAUI
     │
     ↓
SelectedTabColor
     │
     ├── Windows → Componente nativo Windows
     │
     ├── Android → Componente nativo Android
     │
     └── iOS → Componente nativo iOS
```

Como cada plataforma possui componentes visuais próprios, o resultado pode não ser exatamente igual.

---

# 21. Importância da personalização por plataforma

Em aplicações reais, pode ser necessário utilizar configurações específicas para cada sistema.

Por exemplo:

```text
Windows
→ configuração A

Android
→ configuração B

iOS
→ configuração C
```

Isso não significa que precisamos criar aplicativos completamente diferentes.

Podemos manter a maior parte da aplicação compartilhada e fazer ajustes específicos quando necessário.

---

# 22. Principais conceitos da aula

| Conceito             | Explicação                                              |
| -------------------- | ------------------------------------------------------- |
| `TabbedPage`         | Interface baseada em abas                               |
| `BarBackgroundColor` | Define uma cor sólida para o fundo da barra             |
| `BarBackground`      | Define um `Brush` para o fundo                          |
| `Color`              | Representa uma cor                                      |
| `Brush`              | Representa um preenchimento que pode ser mais elaborado |
| `SelectedTabColor`   | Define a cor/aparência da aba selecionada               |
| `UnselectedTabColor` | Define a cor/aparência das abas não selecionadas        |
| `BarTextColor`       | Define a cor dos textos das abas                        |
| `Hexadecimal`        | Permite representar cores usando valores como `#FF0000` |
| `Alpha`              | Permite trabalhar com transparência                     |
| `Gradiente`          | Transição entre diferentes cores                        |
| `Linear Gradient`    | Gradiente seguindo uma direção                          |
| `Radial Gradient`    | Gradiente baseado em um ponto central                   |
| `Multiplataforma`    | O mesmo código pode funcionar em diferentes sistemas    |
| `Componente nativo`  | Elemento visual específico de cada plataforma           |

---

# 23. Resumo final

Nesta aula aprendemos que a `TabbedPage` possui algumas propriedades que permitem personalizar sua aparência.

As quatro propriedades mais importantes apresentadas foram:

```xml
BarBackgroundColor
SelectedTabColor
UnselectedTabColor
BarTextColor
```

Além delas, conhecemos:

```xml
BarBackground
```

que utiliza um `Brush` e permite criar preenchimentos mais elaborados, incluindo gradientes.

Podemos memorizar da seguinte maneira:

```text
BarBackgroundColor
        ↓
Fundo da barra

BarBackground
        ↓
Fundo usando Brush

SelectedTabColor
        ↓
Aba selecionada

UnselectedTabColor
        ↓
Abas não selecionadas

BarTextColor
        ↓
Texto das abas
```

O ponto mais importante da aula é que **essas propriedades podem apresentar comportamentos diferentes em cada sistema operacional**.

Portanto, ao desenvolver uma aplicação .NET MAUI, é importante testar a interface em:

```text
Windows
Android
iOS
macOS
```

e realizar ajustes específicos quando necessário.

A ideia principal é:

> **O .NET MAUI permite compartilhar a interface entre diferentes plataformas, mas a aparência final pode variar porque os controles são apresentados utilizando características e componentes nativos de cada sistema operacional.**