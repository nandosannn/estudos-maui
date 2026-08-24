# Tipos de Páginas no .NET MAUI

## 1. Introdução

No .NET MAUI, as **páginas são a estrutura principal utilizada para construir as telas e a navegação de um aplicativo**.

É dentro das páginas que os componentes visuais são organizados, como:

- `Label`;
    
- `Button`;
    
- `Image`;
    
- `Entry`;
    
- `Border`;
    
- Layouts;
    
- Entre outros componentes.
    

A aula apresenta quatro tipos de páginas/estruturas:

1. `ContentPage`;
    
2. `NavigationPage`;
    
3. `FlyoutPage`;
    
4. `TabbedPage`.
    

Um ponto importante apresentado na aula é que essas estruturas **não precisam necessariamente ser utilizadas de forma isolada**. Elas podem trabalhar em conjunto para formar a estrutura de navegação desejada para o aplicativo.

---

# 2. ContentPage

A primeira estrutura apresentada é a:

```text
ContentPage
```

Também podemos entendê-la como uma **página de conteúdo**.

Ela representa basicamente uma tela onde podemos colocar e organizar os componentes visuais do aplicativo.

Podemos imaginar a `ContentPage` como uma área inicialmente disponível para construirmos nossa interface.

Por exemplo:

```xml
<ContentPage>

    <VerticalStackLayout>

        <Label Text="Número da Sorte" />

        <Button Text="Gerar número" />

    </VerticalStackLayout>

</ContentPage>
```

Nesse exemplo:

```text
ContentPage
    ↓
    Tela
    │
    └── VerticalStackLayout
          ├── Label
          └── Button
```

A `ContentPage` é, portanto, a página onde o conteúdo visual será colocado.

---

# 3. ContentPage no aplicativo Número da Sorte

No projeto desenvolvido anteriormente no curso, foi utilizada uma `ContentPage` para construir a tela do aplicativo **Número da Sorte**.

Dentro dela foram colocados os componentes responsáveis pela interface.

Podemos representar a estrutura de maneira simplificada:

```text
ContentPage
│
└── Layout
    │
    ├── Label
    ├── Elementos visuais
    └── Button
```

Portanto, quando criamos uma tela simples no .NET MAUI, é muito comum começar com uma `ContentPage`.

---

# 4. O que a ContentPage faz?

A principal função da `ContentPage` é **apresentar o conteúdo de uma tela**.

Ela não é, por si só, responsável por criar uma estrutura complexa de navegação.

Seu papel principal é fornecer a página onde os componentes da interface serão organizados.

Podemos resumir:

|Estrutura|Função principal|
|---|---|
|`ContentPage`|Apresentar o conteúdo de uma tela|
|`NavigationPage`|Gerenciar navegação entre páginas|
|`FlyoutPage`|Criar uma estrutura com menu lateral|
|`TabbedPage`|Organizar páginas através de abas|

---

# 5. NavigationPage

A segunda estrutura apresentada é a:

```text
NavigationPage
```

Diferentemente da `ContentPage`, a `NavigationPage` possui como principal objetivo **organizar a navegação entre diferentes páginas**.

Ela fornece uma estrutura de navegação que pode incluir:

- Cabeçalho;
    
- Título;
    
- Botão de voltar;
    
- Navegação entre páginas;
    
- Pilha de páginas visitadas.
    

Podemos imaginar:

```text
NavigationPage
│
├── ContentPage 1
│
├── ContentPage 2
│
└── ContentPage 3
```

A `NavigationPage` funciona como uma estrutura que gerencia o deslocamento entre essas páginas.

---

# 6. Exemplo de navegação

Imagine que o aplicativo tenha três telas:

```text
Tela inicial
     ↓
Tela de cadastro
     ↓
Tela de confirmação
```

O usuário pode navegar:

```text
ContentPage 1
      ↓
ContentPage 2
      ↓
ContentPage 3
```

Depois, pode voltar:

```text
ContentPage 3
      ↓
ContentPage 2
      ↓
ContentPage 1
```

Essa estrutura de navegação é o papel da `NavigationPage`.

---

# 7. Cabeçalho da NavigationPage

Uma característica apresentada na aula é a presença de uma estrutura superior, que pode apresentar informações como:

```text
┌─────────────────────────────┐
│ ←  Número da Sorte          │
├─────────────────────────────┤
│                             │
│       Conteúdo da tela      │
│                             │
└─────────────────────────────┘
```

Nessa área podemos ter:

- Título da página;
    
- Botão para voltar;
    
- Outros elementos relacionados à navegação.
    

A própria plataforma também pode fornecer mecanismos para voltar à página anterior, como o botão de voltar do Android.

---

# 8. NavigationPage e ContentPage

Um ponto importante da aula é entender que a `NavigationPage` não substitui a `ContentPage`.

Elas possuem responsabilidades diferentes.

Podemos pensar:

```text
NavigationPage
     ↓
Responsável pela navegação
     ↓
ContentPage
     ↓
Responsável pelo conteúdo
```

Por exemplo:

```text
NavigationPage
│
├── ContentPage
│    └── Tela inicial
│
├── ContentPage
│    └── Cadastro
│
└── ContentPage
     └── Configurações
```

Portanto, a `ContentPage` pode ser utilizada dentro de uma estrutura de navegação.

---

# 9. FlyoutPage

A terceira estrutura apresentada é a:

```text
FlyoutPage
```

Ela é utilizada para criar uma interface que possui um **menu lateral**.

Esse tipo de estrutura é conhecido em algumas plataformas como:

```text
Drawer
```

ou menu de gaveta.

A ideia é permitir que o usuário abra um menu lateral para acessar diferentes partes do aplicativo.

---

# 10. Funcionamento do FlyoutPage

Podemos imaginar uma aplicação com várias opções:

```text
Menu
├── Início
├── Perfil
├── Configurações
├── Relatórios
└── Sobre
```

O usuário pode abrir o menu lateral e escolher uma dessas opções.

Visualmente:

```text
┌──────────────────────────────┐
│ Menu                         │
│                              │
│ Início                       │
│ Perfil                       │
│ Configurações                │
│ Relatórios                   │
│ Sobre                        │
│                              │
└──────────────────────────────┘
```

Quando o menu está fechado, o conteúdo principal ocupa a tela.

Quando o usuário abre o menu, ele aparece sobre ou ao lado do conteúdo.

---

# 11. Quando utilizar o FlyoutPage?

A estrutura de menu lateral é especialmente interessante quando temos um aplicativo com **várias áreas e opções de navegação**.

Por exemplo:

```text
Aplicativo
│
├── Início
├── Usuários
├── Produtos
├── Relatórios
├── Configurações
└── Perfil
```

Em vez de colocar todas essas opções em uma barra inferior, podemos utilizar um menu lateral.

Assim, o `FlyoutPage` ajuda a organizar aplicações com muitas opções.

---

# 12. TabbedPage

A quarta estrutura apresentada é a:

```text
TabbedPage
```

Ela organiza diferentes páginas por meio de **abas**.

Essas abas podem aparecer na parte inferior ou superior, dependendo da configuração e da plataforma.

Um exemplo visual seria:

```text
┌──────────────────────────────┐
│                              │
│       Conteúdo da tela       │
│                              │
│                              │
├────────┬───────────┬─────────┤
│ Início │ Perfil    │ Config. │
└────────┴───────────┴─────────┘
```

O usuário pode tocar em uma aba para trocar de página.

---

# 13. Exemplo de TabbedPage

Imagine um aplicativo com três áreas principais:

```text
Início
Perfil
Configurações
```

Podemos organizar:

```text
TabbedPage
│
├── ContentPage → Início
├── ContentPage → Perfil
└── ContentPage → Configurações
```

Cada aba representa uma página de conteúdo.

Portanto, assim como acontece com a `NavigationPage`, a `TabbedPage` pode trabalhar com `ContentPage`.

---

# 14. ContentPage como base do conteúdo

Um dos pontos mais importantes apresentados na aula é perceber que a `ContentPage` aparece como a página responsável pelo conteúdo propriamente dito.

As outras estruturas fornecem mecanismos de organização e navegação.

Podemos representar:

```text
ContentPage
    ↓
Conteúdo da tela

NavigationPage
    ↓
Navegação

FlyoutPage
    ↓
Menu lateral

TabbedPage
    ↓
Abas
```

Isso facilita a compreensão das responsabilidades de cada estrutura.

---

# 15. As páginas podem trabalhar em conjunto

As estruturas apresentadas não precisam ser utilizadas individualmente.

Elas podem ser combinadas.

Por exemplo:

```text
FlyoutPage
│
├── Menu lateral
│
└── NavigationPage
      │
      ├── ContentPage
      ├── ContentPage
      └── ContentPage
```

Nesse caso temos:

- `FlyoutPage` → responsável pelo menu lateral;
    
- `NavigationPage` → responsável pela navegação;
    
- `ContentPage` → responsável pelo conteúdo das telas.
    

---

# 16. Outro exemplo de combinação

Também podemos utilizar uma estrutura com abas e navegação.

Por exemplo:

```text
TabbedPage
│
├── NavigationPage
│     ├── ContentPage
│     └── ContentPage
│
├── NavigationPage
│     └── ContentPage
│
└── ContentPage
```

A ideia principal é que essas estruturas podem ser combinadas para atender à necessidade da aplicação.

---

# 17. As estruturas não se excluem

Esse é um conceito importante da aula.

Não devemos pensar:

```text
OU ContentPage
OU NavigationPage
OU FlyoutPage
OU TabbedPage
```

Como se fosse necessário escolher somente uma.

É possível trabalhar com combinações:

```text
FlyoutPage
     +
NavigationPage
     +
ContentPage
```

ou:

```text
TabbedPage
     +
NavigationPage
     +
ContentPage
```

A combinação dependerá da estrutura de navegação que queremos construir.

---

# 18. Comparação entre as quatro estruturas

|Tipo|Principal finalidade|Exemplo|
|---|---|---|
|`ContentPage`|Exibir conteúdo|Tela de login|
|`NavigationPage`|Navegar entre páginas|Tela → Cadastro → Confirmação|
|`FlyoutPage`|Criar menu lateral|Aplicativo com várias áreas|
|`TabbedPage`|Navegar por abas|Início / Perfil / Configurações|

---

# 19. Exemplo de arquitetura

Um aplicativo mais completo poderia ter uma estrutura semelhante a:

```text
Aplicativo
│
└── FlyoutPage
    │
    ├── Menu
    │   ├── Início
    │   ├── Produtos
    │   ├── Relatórios
    │   └── Configurações
    │
    └── NavigationPage
        │
        ├── ContentPage
        │     └── Início
        │
        ├── ContentPage
        │     └── Produtos
        │
        └── ContentPage
              └── Detalhes do produto
```

Nesse cenário:

### `FlyoutPage`

Controla o menu lateral.

### `NavigationPage`

Controla a navegação entre as telas.

### `ContentPage`

Apresenta o conteúdo de cada tela.

---

# 20. Como escolher cada estrutura?

Podemos utilizar uma regra simples:

### Quero apenas uma tela de conteúdo

Utilize:

```text
ContentPage
```

Exemplo:

```text
Aplicativo Número da Sorte
        ↓
ContentPage
```

---

### Quero navegar entre várias telas

Uma estrutura de navegação pode ser utilizada:

```text
NavigationPage
```

Exemplo:

```text
Login
 ↓
Cadastro
 ↓
Perfil
```

---

### Tenho muitas opções e quero um menu lateral

Utilize:

```text
FlyoutPage
```

Exemplo:

```text
Menu lateral
├── Início
├── Usuários
├── Relatórios
└── Configurações
```

---

### Tenho poucas áreas principais e quero abas

Utilize:

```text
TabbedPage
```

Exemplo:

```text
[Início] [Perfil] [Configurações]
```

---

# 21. Relação com o aplicativo Número da Sorte

O aplicativo desenvolvido anteriormente utiliza uma estrutura mais simples.

Podemos representá-lo:

```text
ContentPage
│
└── Layout
    │
    ├── Título
    ├── Números
    └── Botão
```

Como o aplicativo possui basicamente uma tela principal, não existe necessidade de uma estrutura complexa de navegação para o funcionamento básico apresentado.

Em aplicativos maiores, entretanto, podemos precisar combinar diferentes estruturas.

---

# 22. Resumo dos conceitos

|Conceito|O que faz?|
|---|---|
|`ContentPage`|Representa uma página de conteúdo|
|`NavigationPage`|Organiza a navegação entre páginas|
|`FlyoutPage`|Oferece uma estrutura com menu lateral|
|`TabbedPage`|Organiza páginas através de abas|
|Navegação|Permite passar de uma tela para outra|
|Menu lateral|Apresenta opções de navegação em uma área lateral|
|Abas|Permitem alternar entre diferentes áreas do aplicativo|
|Combinação de páginas|Permite criar estruturas de navegação mais complexas|

---

# 23. Estrutura mental para memorizar

Uma forma simples de memorizar o conteúdo é:

```text
CONTENT
↓
O que aparece na tela?

NAVIGATION
↓
Como eu navego entre telas?

FLYOUT
↓
Como eu acesso um menu lateral?

TABS
↓
Como eu acesso diferentes áreas através de abas?
```

Ou:

```text
ContentPage  → Conteúdo
NavigationPage → Navegação
FlyoutPage → Menu lateral
TabbedPage → Abas
```

---

# 24. Principal aprendizado da aula

O principal aprendizado é entender que **páginas são a estrutura fundamental para construir aplicações no .NET MAUI**.

A `ContentPage` é utilizada para apresentar o conteúdo da tela, enquanto estruturas como `NavigationPage`, `FlyoutPage` e `TabbedPage` fornecem diferentes formas de organizar a navegação.

Essas estruturas podem ser utilizadas em conjunto.

Por exemplo:

```text
FlyoutPage
     ↓
NavigationPage
     ↓
ContentPage
```

Isso significa:

```text
Menu lateral
     ↓
Sistema de navegação
     ↓
Tela de conteúdo
```

Essa possibilidade de combinação permite criar desde aplicações simples, como o **Número da Sorte**, até aplicações maiores com diversas telas, menus, abas e diferentes níveis de navegação.

---

# 25. Resumo final

O .NET MAUI oferece diferentes estruturas para organizar as telas e a navegação das aplicações.

A `ContentPage` representa uma página de conteúdo e é utilizada para colocar os componentes visuais da aplicação.

A `NavigationPage` é voltada para a navegação entre diferentes páginas, podendo apresentar cabeçalho, título e mecanismos de retorno.

A `FlyoutPage` permite criar um menu lateral, sendo útil principalmente em aplicações com muitas opções ou áreas.

A `TabbedPage` organiza diferentes páginas por meio de abas, sendo interessante quando o aplicativo possui algumas áreas principais que precisam ser acessadas rapidamente.

O ponto mais importante é que essas estruturas **podem ser combinadas**. Uma aplicação pode utilizar, por exemplo, um `FlyoutPage` para o menu lateral, uma `NavigationPage` para controlar a navegação e várias `ContentPage` para apresentar o conteúdo.

```text
                 APLICAÇÃO
                     │
             ┌───────┴───────┐
             │               │
         Navegação        Conteúdo
             │               │
     ┌───────┼───────┐       │
     │       │       │       │
  Flyout  Tabs   Navigation  │
                     │        │
                     └───────► ContentPage
```

Portanto, a escolha da estrutura depende da experiência de navegação que queremos oferecer ao usuário.