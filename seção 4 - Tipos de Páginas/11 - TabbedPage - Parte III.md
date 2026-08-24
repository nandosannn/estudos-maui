# Customização da TabbedPage no Android — .NET MAUI

## 1. Objetivo da aula

Nesta aula aprendemos como adaptar a aparência da `TabbedPage` para o Android.

O principal ponto é entender que uma configuração feita no Windows pode não apresentar o mesmo resultado no Android.

A aula trabalha principalmente:

- diferenças visuais entre plataformas;
    
- customização específica para Android;
    
- utilização de `Color`;
    
- utilização de `Colors`;
    
- personalização das cores das abas;
    
- utilização de recursos específicos da plataforma;
    
- alteração da posição das abas;
    
- utilização de ícones;
    
- utilização de imagens SVG;
    
- combinação entre diferentes tipos de páginas;
    
- reinicialização e recarga do aplicativo.
    

---

# 2. Diferença entre Windows e Android

No Windows, algumas propriedades utilizadas anteriormente apresentavam um determinado resultado visual.

Por exemplo:

```xml
SelectedTabColor
UnselectedTabColor
```

No Windows, poderíamos ter algo semelhante a:

```text
Página 1 | Página 2 | Página 3
████████
  verde
```

Enquanto as abas não selecionadas poderiam apresentar outra cor:

```text
Página 1 | Página 2 | Página 3
  verde      cinza      cinza
```

No Android, entretanto, essas propriedades podem apresentar outro comportamento.

Isso ocorre porque o .NET MAUI trabalha com componentes nativos de cada sistema operacional.

Podemos representar:

```text
                    .NET MAUI
                        │
             ┌──────────┴──────────┐
             │                     │
          Windows                Android
             │                     │
       Componente nativo     Componente nativo
             │                     │
        Aparência A           Aparência B
```

Portanto:

> Uma propriedade do .NET MAUI não necessariamente terá exatamente o mesmo resultado visual em todas as plataformas.

---

# 3. Componentes nativos

Cada sistema operacional possui seus próprios componentes visuais.

Por isso, o .NET MAUI precisa adaptar os controles para cada plataforma.

Podemos pensar:

```text
Código MAUI
     ↓
Controle MAUI
     ↓
Adaptação para plataforma
     ↓
Componente nativo
```

Consequentemente:

```text
Windows → comportamento visual próprio
Android → comportamento visual próprio
iOS     → comportamento visual próprio
macOS   → comportamento visual próprio
```

Isso explica por que uma configuração pode funcionar muito bem no Windows e não apresentar o mesmo resultado no Android.

---

# 4. Cuidado com BarTextColor no Android

Um dos principais pontos apresentados na aula foi o cuidado com:

```xml
BarTextColor
```

No Android, essa propriedade pode alterar o texto de **todas as abas**, tanto as selecionadas quanto as não selecionadas.

Por exemplo:

```xml
BarTextColor="White"
```

pode produzir:

```text
Página 1 | Página 2 | Página 3
  branco     branco     branco
```

Isso pode prejudicar a diferenciação entre a aba selecionada e as demais.

Por esse motivo, a recomendação apresentada foi:

> No Android, evite utilizar `BarTextColor` quando ele prejudicar a distinção visual entre as abas.

---

# 5. Removendo BarTextColor

Se tivermos:

```xml
BarTextColor="White"
```

podemos simplesmente remover essa propriedade.

Antes:

```text
Página 1 | Página 2 | Página 3
  branco     branco     branco
```

Depois de remover:

```text
Página 1 | Página 2 | Página 3
  comportamento nativo do Android
```

Isso permite que o próprio Android controle melhor a aparência dos textos.

---

# 6. Customizando as cores

A aula também mostra como utilizar as cores disponibilizadas pelo próprio .NET MAUI.

Por exemplo:

```xml
SelectedTabColor="Purple"
```

Ou utilizando um valor hexadecimal:

```xml
SelectedTabColor="#512BD4"
```

O valor apresentado na aula foi associado à cor roxa utilizada pelo .NET MAUI.

Assim:

```text
SelectedTabColor
        ↓
Cor da aba selecionada
        ↓
Roxo
```

---

# 7. Utilizando Colors

O .NET MAUI disponibiliza uma classe chamada:

```text
Colors
```

Ela contém diversas cores prontas que podem ser utilizadas na aplicação.

Exemplos:

```text
Colors.Red
Colors.Blue
Colors.Green
Colors.Purple
Colors.Gray
Colors.White
Colors.Black
```

No XAML, também podemos utilizar nomes de cores diretamente.

Por exemplo:

```xml
SelectedTabColor="Purple"
```

---

# 8. UnselectedTabColor

A propriedade:

```xml
UnselectedTabColor
```

permite definir a aparência das abas que não estão selecionadas.

Exemplo:

```xml
UnselectedTabColor="Gray"
```

Teríamos:

```text
Página 1 | Página 2 | Página 3
  roxo       cinza      cinza
```

Se selecionarmos a Página 2:

```text
Página 1 | Página 2 | Página 3
  cinza      roxo       cinza
```

Ou seja:

```text
SelectedTabColor
        ↓
Aba selecionada

UnselectedTabColor
        ↓
Abas não selecionadas
```

---

# 9. Cores específicas para o Android

A aula mostra que algumas configurações precisam ser feitas diretamente nos recursos da plataforma.

No caso do Android, podemos trabalhar com arquivos específicos da plataforma.

Um exemplo importante são os recursos de cores do Android.

A ideia é:

```text
Resources
   │
   └── Colors
          │
          ├── ColorPrimary
          ├── ColorPrimaryDark
          └── ColorAccent
```

Essas cores são utilizadas pelo Android em diferentes partes da interface.

---

# 10. ColorPrimary

Uma das cores apresentadas foi:

```text
ColorPrimary
```

Ela pode ser utilizada pelo Android em diversos componentes.

Por exemplo, a cor da seleção da aba pode estar relacionada à cor primária do aplicativo.

Podemos representar:

```text
ColorPrimary
     ↓
Componentes Android
     ↓
Elementos de destaque
```

Alterando essa cor, podemos modificar determinados elementos visuais do aplicativo.

---

# 11. ColorPrimaryDark

Outra configuração existente nos recursos do Android é:

```text
ColorPrimaryDark
```

Ela está relacionada a áreas mais escuras ou elementos específicos do tema do Android.

O resultado exato depende do componente e da versão/tema utilizados.

O conceito principal da aula é:

> Algumas características visuais precisam ser configuradas diretamente nos recursos nativos da plataforma.

---

# 12. ColorAccent

Também existe:

```text
ColorAccent
```

Ela pode ser utilizada para elementos que precisam de maior destaque.

Podemos pensar:

```text
ColorPrimary
     ↓
Cor principal

ColorPrimaryDark
     ↓
Variação mais escura

ColorAccent
     ↓
Cor de destaque
```

Essas configurações fazem parte da personalização específica do Android.

---

# 13. Ícones nas abas

Além das cores, a aula mostra como adicionar ícones às abas.

A ideia é utilizar uma imagem para representar cada página.

Por exemplo:

```text
   ●1        ●2        ●3
Página 1  Página 2  Página 3
```

Isso melhora a identificação visual das funcionalidades.

---

# 14. Obtendo ícones

Na aula foi utilizado o site IconFinder para encontrar imagens e ícones.

A ideia é procurar imagens que representem a funcionalidade de cada aba.

Por exemplo:

```text
Página 1 → ícone 1
Página 2 → ícone 2
Página 3 → ícone 3
```

O importante é que o ícone tenha relação com a funcionalidade apresentada.

---

# 15. Pasta Images

Depois de obter as imagens, elas são adicionadas à pasta:

```text
Resources/Images
```

Estrutura:

```text
Projeto
│
└── Resources
    │
    └── Images
        ├── 1.svg
        ├── 2.svg
        └── 3.svg
```

O .NET MAUI utiliza essa pasta para gerenciar imagens do aplicativo.

---

# 16. Utilizando SVG

Os ícones utilizados na aula estavam no formato:

```text
.svg
```

O SVG é um formato vetorial.

Uma vantagem é que ele pode ser utilizado para gerar diferentes resoluções e densidades.

A ideia apresentada na aula é:

```text
SVG
 ↓
.NET MAUI
 ↓
Processamento dos recursos
 ↓
Diferentes dispositivos
```

Isso facilita o trabalho com diferentes tamanhos de tela e densidades.

---

# 17. ImageSource

Para associar um ícone à aba, utilizamos:

```xml
IconImageSource
```

Essa propriedade pode ser colocada na própria página.

Por exemplo:

```xml
<ContentPage
    Title="Página 1"
    IconImageSource="1.png">
```

A página terá:

```text
Título → Página 1
Ícone  → 1.png
```

Essas informações serão utilizadas pela `TabbedPage`.

---

# 18. Exemplo com três páginas

Página 1:

```xml
<ContentPage
    Title="Página 1"
    IconImageSource="1.png">
```

Página 2:

```xml
<ContentPage
    Title="Página 2"
    IconImageSource="2.png">
```

Página 3:

```xml
<ContentPage
    Title="Página 3"
    IconImageSource="3.png">
```

A `TabbedPage` poderá apresentar:

```text
┌─────────────────────────────────────┐
│ ① Página 1 | ② Página 2 | ③ Página 3 │
└─────────────────────────────────────┘
```

---

# 19. Por que utilizar ícones?

Os ícones ajudam o usuário a identificar rapidamente a funcionalidade.

Por exemplo:

```text
🏠 Início
🔍 Pesquisa
⚙ Configurações
```

Em vez de depender apenas do texto:

```text
Início | Pesquisa | Configurações
```

O ideal é escolher ícones que tenham relação direta com a função da aba.

---

# 20. Alterando a posição das abas no Android

Outro recurso importante apresentado na aula é a possibilidade de colocar as abas na parte inferior da tela.

Normalmente:

```text
┌─────────────────────┐
│ Página 1 | Página 2 │
├─────────────────────┤
│                     │
│      Conteúdo       │
│                     │
└─────────────────────┘
```

Podemos configurar para:

```text
┌─────────────────────┐
│                     │
│      Conteúdo       │
│                     │
├─────────────────────┤
│ Página 1 | Página 2 │
└─────────────────────┘
```

Esse tipo de navegação é bastante comum em aplicativos móveis.

---

# 21. Namespace específico do Android

Para acessar recursos específicos do Android, podemos utilizar um namespace da plataforma.

A ideia é criar algo semelhante a:

```xml
xmlns:android="..."
```

Esse namespace permite acessar recursos específicos do Android no XAML.

O conceito importante é:

```text
XAML compartilhado
       │
       ├── Recursos gerais do MAUI
       │
       └── Recursos específicos do Android
```

---

# 22. Maui.Controls para Android

Na aula é apresentado um namespace relacionado ao .NET MAUI e à plataforma Android.

Através dele podemos acessar propriedades específicas do Android.

Isso permite fazer:

```text
Configuração geral
        +
Configuração específica do Android
```

sem precisar abandonar completamente o XAML compartilhado.

---

# 23. TabbedPage e BarPlacement

A propriedade específica apresentada permite controlar a posição da barra de abas.

A ideia é utilizar algo semelhante a:

```xml
BarPlacement
```

Podemos pensar em duas possibilidades:

```text
Top
 ↓
Abas na parte superior

Bottom
 ↓
Abas na parte inferior
```

---

# 24. Abas na parte inferior

A configuração apresentada na aula faz com que as abas sejam posicionadas na parte inferior.

Conceitualmente:

```xml
BarPlacement="Bottom"
```

Resultado:

```text
┌─────────────────────────┐
│                         │
│        Conteúdo         │
│                         │
│                         │
├─────────────────────────┤
│ Página 1 | Página 2 | 3 │
└─────────────────────────┘
```

Esse comportamento é muito comum em aplicativos móveis.

---

# 25. Configuração específica por plataforma

Essa parte é muito importante para entender o desenvolvimento multiplataforma.

Podemos ter:

```text
Código compartilhado
        │
        ├── Windows
        │
        ├── Android
        │
        └── iOS
```

E cada plataforma pode receber uma configuração diferente.

Por exemplo:

```text
Windows
→ abas superiores

Android
→ abas inferiores

iOS
→ abas inferiores
```

Isso permite adaptar a interface ao padrão visual esperado pelos usuários de cada plataforma.

---

# 26. Necessidade de reiniciar o aplicativo

Algumas alterações não são aplicadas pela recarga dinâmica.

Isso acontece principalmente quando modificamos configurações nativas da plataforma.

Por exemplo:

```text
Alteração comum de XAML
        ↓
Hot Reload pode atualizar

Alteração nativa
        ↓
Pode exigir reinicialização
```

Por isso, após alterar configurações específicas do Android, pode ser necessário reiniciar o aplicativo.

---

# 27. Reiniciar o projeto x reiniciar o aplicativo

A aula apresenta duas formas de reinicialização.

|Opção|Atalho/ação|Característica|
|---|---|---|
|Reiniciar projeto|`Ctrl + Shift + F5`|Pode recompilar uma quantidade maior de elementos|
|Reiniciar aplicativo|Botão de reinicialização|Geralmente mais rápido|
|Hot Reload|Recarga dinâmica|Atualiza alterações compatíveis sem reiniciar completamente|

A ideia principal é utilizar a opção mais rápida quando a alteração permitir.

---

# 28. Hot Reload

O Hot Reload permite visualizar determinadas alterações sem precisar reconstruir completamente o aplicativo.

Fluxo:

```text
Alterar XAML
     ↓
Hot Reload
     ↓
Atualização da interface
```

Porém, nem todas as alterações são compatíveis com Hot Reload.

Configurações nativas ou estruturais podem exigir uma nova compilação.

---

# 29. Reinicialização mais rápida

Quando o Hot Reload não consegue atualizar uma alteração, podemos utilizar a opção de reiniciar o aplicativo.

Essa opção pode aproveitar arquivos que já foram compilados.

Podemos pensar:

```text
Projeto completo
↓
Compilar tudo
↓
Mais demorado
```

Enquanto:

```text
Reiniciar aplicativo
↓
Aproveitar arquivos já compilados
↓
Mais rápido
```

O tempo exato depende do projeto, computador e configuração.

---

# 30. Combinação dos tipos de páginas

No final da aula, é apresentado um conceito muito importante:

> Os diferentes tipos de páginas do .NET MAUI podem trabalhar em conjunto.

Não precisamos escolher apenas um modelo de navegação para todo o aplicativo.

Podemos combinar:

```text
TabbedPage
NavigationPage
FlyoutPage
ContentPage
```

---

# 31. Exemplo de combinação

Podemos ter:

```text
TabbedPage
│
├── NavigationPage
│     └── Página 1
│
├── NavigationPage
│     └── Página 2
│
└── FlyoutPage
      ├── Menu lateral
      └── Detail
```

Isso significa que cada aba pode ter uma estrutura de navegação diferente.

---

# 32. Exemplo prático

Imagine um aplicativo com três abas:

```text
┌──────────────────────────────────┐
│ Início | Produtos | Configurações│
└──────────────────────────────────┘
```

A aba **Início** poderia utilizar:

```text
NavigationPage
```

A aba **Produtos** também:

```text
NavigationPage
```

E a aba **Configurações** poderia utilizar uma estrutura diferente.

Assim:

```text
TabbedPage
│
├── Início
│    └── NavigationPage
│
├── Produtos
│    └── NavigationPage
│
└── Configurações
     └── FlyoutPage
```

---

# 33. Aplicações reais

A combinação de diferentes formas de navegação é bastante comum em aplicativos grandes.

Um aplicativo pode possuir:

```text
Abas inferiores
       +
Menu lateral
       +
Navegação entre páginas
```

Isso permite criar estruturas complexas sem depender de apenas um tipo de navegação.

A aula cita aplicativos conhecidos como referência de conceitos de navegação, como aplicativos do Google e o YouTube.

---

# 34. Resumo das propriedades

|Propriedade/Recurso|Função|
|---|---|
|`SelectedTabColor`|Define a aparência da aba selecionada|
|`UnselectedTabColor`|Define a aparência das abas não selecionadas|
|`BarTextColor`|Altera a cor dos textos das abas|
|`IconImageSource`|Define o ícone da página/aba|
|`BarPlacement`|Define a posição da barra de abas em plataformas que oferecem esse recurso|
|`Colors`|Fornece cores predefinidas|
|`ColorPrimary`|Cor principal utilizada em recursos do Android|
|`ColorPrimaryDark`|Variação escura da cor principal|
|`ColorAccent`|Cor utilizada para elementos de destaque|
|`Brush`|Permite preenchimentos mais elaborados|
|`SVG`|Formato vetorial utilizado nos ícones|
|`Hot Reload`|Permite atualizar alterações compatíveis sem recompilar tudo|
|Namespace específico|Permite acessar recursos de uma plataforma específica|

---

# 35. Estrutura mental da aula

```text
                  TabbedPage
                      │
          ┌───────────┴───────────┐
          │                       │
       Visual                  Navegação
          │                       │
    ┌─────┼─────┐          ┌──────┼──────┐
    │     │     │          │      │      │
  Cores Ícones Posição   Tabs   Navigation Flyout
    │     │     │
    │     │     └── Bottom
    │     │
    │     └── IconImageSource
    │
    ├── SelectedTabColor
    ├── UnselectedTabColor
    └── BarTextColor
```

---

# 36. Exemplo de configuração conceitual

Uma `TabbedPage` pode possuir configurações gerais e específicas do Android:

```xml
<TabbedPage
    ...
    SelectedTabColor="Purple"
    UnselectedTabColor="Gray">

    <ContentPage
        Title="Página 1"
        IconImageSource="1.png">

        <!-- Conteúdo -->

    </ContentPage>

    <ContentPage
        Title="Página 2"
        IconImageSource="2.png">

        <!-- Conteúdo -->

    </ContentPage>

    <ContentPage
        Title="Página 3"
        IconImageSource="3.png">

        <!-- Conteúdo -->

    </ContentPage>

</TabbedPage>
```

O resultado esperado seria uma estrutura semelhante a:

```text
┌─────────────────────────────┐
│                             │
│          Conteúdo           │
│                             │
│                             │
├─────────────────────────────┤
│ ① Página 1  ② Página 2  ③ │
└─────────────────────────────┘
```

No Android, configurações específicas podem alterar a posição e a aparência dessa barra.

---

# 37. Principais aprendizados

1. **A mesma propriedade pode ter resultados diferentes em cada plataforma.**
    
2. **O Android possui recursos específicos para personalização.**
    
3. **`BarTextColor` deve ser utilizado com cuidado no Android.**
    
4. **`SelectedTabColor` e `UnselectedTabColor` podem ser utilizados para diferenciar as abas.**
    
5. **As páginas podem possuir ícones utilizando `IconImageSource`.**
    
6. **Imagens SVG podem ser utilizadas como recursos do aplicativo.**
    
7. **É possível configurar a barra de abas para ficar na parte inferior no Android.**
    
8. **Algumas configurações específicas da plataforma exigem reinicialização do aplicativo.**
    
9. **Hot Reload é útil, mas não consegue atualizar todas as alterações.**
    
10. **Os diferentes modelos de página podem ser combinados.**
    

---

# 38. Resumo final

A principal ideia desta aula é que desenvolver com .NET MAUI não significa apenas escrever um código único e esperar que todas as plataformas tenham exatamente a mesma aparência.

O .NET MAUI permite compartilhar grande parte do código, mas cada sistema operacional possui suas próprias características.

Podemos pensar:

```text
                    .NET MAUI
                        │
             Código compartilhado
                        │
          ┌─────────────┼─────────────┐
          ↓             ↓             ↓
       Windows       Android          iOS
          │             │             │
       Visual A      Visual B       Visual C
```

No Android, aprendemos a:

```text
✓ Ajustar as cores
✓ Evitar BarTextColor quando ele prejudica a aparência
✓ Utilizar recursos nativos do Android
✓ Alterar a posição das abas
✓ Colocar as abas na parte inferior
✓ Adicionar ícones
✓ Utilizar imagens SVG
✓ Trabalhar com configurações específicas da plataforma
✓ Combinar TabbedPage com NavigationPage e FlyoutPage
```

A ideia mais importante para guardar é:

> **O .NET MAUI permite compartilhar código entre plataformas, mas também fornece mecanismos para adaptar a interface às características específicas de cada sistema operacional.**