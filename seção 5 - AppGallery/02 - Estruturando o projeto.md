# .NET MAUI — Estrutura Inicial do MAUI Gallery com FlyoutPage

## 1. Objetivo da aula

Nesta etapa, o projeto **MAUI Gallery** começa a receber sua estrutura de navegação.

A estrutura será baseada em:

- `FlyoutPage` → estrutura principal do aplicativo;
    
- `Menu` → conteúdo do menu lateral;
    
- `MainPage` → página principal;
    
- `NavigationPage` → responsável pela navegação e barra de título;
    
- `Views` → pasta para organizar as páginas do aplicativo.
    

A estrutura ficará aproximadamente assim:

```text
MAUI Gallery
│
├── Views
│   ├── MainPage.xaml
│   └── Menu.xaml
│
├── App.xaml
├── App.xaml.cs
│
└── AppFlyOut.xaml
    AppFlyOut.xaml.cs
```

---

# 2. Remoção do AppShell e MainPage antigos

Como o projeto padrão do .NET MAUI utiliza o `AppShell`, a primeira alteração foi remover:

```text
AppShell.xaml
AppShell.xaml.cs
MainPage.xaml
MainPage.xaml.cs
```

A ideia é abandonar a estrutura padrão do projeto e criar uma estrutura personalizada utilizando `FlyoutPage`.

---

# 3. Criação da pasta `Views`

Para melhorar a organização do projeto, foi criada uma pasta chamada:

```text
Views
```

Essa pasta será responsável por armazenar as páginas da aplicação.

Dentro dela serão colocadas inicialmente:

```text
Views
│
├── MainPage.xaml
├── MainPage.xaml.cs
│
├── Menu.xaml
└── Menu.xaml.cs
```

### Organização

| Pasta      | Responsabilidade                              |
| ---------- | --------------------------------------------- |
| `Views`    | Armazenar as páginas/interfaces do aplicativo |
| `MainPage` | Página principal                              |
| `Menu`     | Conteúdo do menu lateral                      |

Essa organização facilita a manutenção do projeto conforme o número de páginas aumenta.

---

# 4. Criação da `MainPage`

A primeira página criada dentro de `Views` foi:

```text
MainPage
```

Ela será uma:

```text
ContentPage
```

Sua função será representar a **página principal do aplicativo**.

Exemplo:

```xml
<ContentPage>
    <!-- Conteúdo da página inicial -->
</ContentPage>
```

---

# 5. Criação da página `Menu`

Também foi criada uma página chamada:

```text
Menu
```

Ela também é uma:

```text
ContentPage
```

Sua finalidade é representar o conteúdo que será exibido no **menu lateral do FlyoutPage**.

Estrutura:

```text
Views
├── MainPage
└── Menu
```

---

# 6. Criação do `FlyoutPage`

Na raiz do projeto foi criado um novo arquivo para representar a estrutura principal:

```text
AppFlyOut
```

Esse arquivo será responsável por controlar o menu lateral e a página principal.

A estrutura pode ser representada assim:

```text
AppFlyOut
│
├── Flyout
│   └── Menu
│
└── Detail
    └── MainPage
```

---

# 7. `FlyoutPage`

O `FlyoutPage` possui duas partes principais:

|Propriedade|Função|
|---|---|
|`Flyout`|Representa o menu lateral|
|`Detail`|Representa o conteúdo principal|

Podemos visualizar assim:

```text
┌───────────────────────────────┐
│           FlyoutPage           │
├──────────────┬────────────────┤
│              │                │
│   Flyout     │     Detail     │
│              │                │
│    Menu      │   MainPage     │
│              │                │
└──────────────┴────────────────┘
```

---

# 8. Configuração do XAML

O arquivo `AppFlyOut.xaml` precisa utilizar `FlyoutPage` como elemento principal.

Exemplo conceitual:

```xml
<FlyoutPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="MauiGallery.AppFlyOut">

    <FlyoutPage.Flyout>
        <views:Menu />
    </FlyoutPage.Flyout>

    <FlyoutPage.Detail>
        <NavigationPage>
            <x:Arguments>
                <views:MainPage />
            </x:Arguments>
        </NavigationPage>
    </FlyoutPage.Detail>

</FlyoutPage>
```

---

# 9. Importação do namespace `Views`

Como `MainPage` e `Menu` estão dentro da pasta `Views`, é necessário importar o namespace correspondente.

Exemplo:

```xml
xmlns:views="clr-namespace:MauiGallery.Views"
```

Depois disso, podemos utilizar:

```xml
<views:Menu />
```

e:

```xml
<views:MainPage />
```

### Por que isso é necessário?

O namespace permite que o XAML encontre as classes que foram criadas dentro da pasta `Views`.

---

# 10. `Flyout`

A propriedade:

```xml
<FlyoutPage.Flyout>
```

define qual página será utilizada como **menu lateral**.

Neste projeto:

```xml
<FlyoutPage.Flyout>
    <views:Menu />
</FlyoutPage.Flyout>
```

Portanto:

```text
Flyout
   ↓
Menu
```

---

# 11. `Detail`

A propriedade:

```xml
<FlyoutPage.Detail>
```

define qual será o **conteúdo principal** apresentado ao usuário.

Neste projeto, foi utilizada uma `NavigationPage`:

```xml
<FlyoutPage.Detail>
    <NavigationPage>
        <x:Arguments>
            <views:MainPage />
        </x:Arguments>
    </NavigationPage>
</FlyoutPage.Detail>
```

A estrutura fica:

```text
Detail
  ↓
NavigationPage
  ↓
MainPage
```

---

# 12. Por que utilizar `NavigationPage`?

A `NavigationPage` adiciona recursos de navegação à página principal.

Entre eles está a **barra de título/navegação** apresentada na interface.

A estrutura utilizada é:

```text
FlyoutPage
    │
    ├── Flyout
    │    └── Menu
    │
    └── Detail
         └── NavigationPage
              └── MainPage
```

Assim, o aplicativo combina:

- Menu lateral;
    
- Navegação;
    
- Página principal.
    

---

# 13. Alteração do `App.xaml.cs`

Depois de criar o `AppFlyOut`, é necessário informar ao aplicativo qual será a estrutura inicial.

Anteriormente, o projeto poderia utilizar:

```csharp
MainPage = new AppShell();
```

Agora será utilizada a estrutura criada:

```csharp
MainPage = new AppFlyOut();
```

Ou seja:

```text
Aplicativo inicia
      ↓
App
      ↓
AppFlyOut
      ↓
FlyoutPage
      ├── Menu
      └── MainPage
```

---

# 14. Configuração do `FlyoutLayoutBehavior`

Foi adicionada uma configuração para controlar o comportamento do menu lateral:

```xml
FlyoutLayoutBehavior="Popover"
```

O objetivo é fazer com que o menu seja **recolhido e expandido**, inclusive no Windows.

### Comportamento `Popover`

Quando o menu está fechado:

```text
┌─────────────────────────────┐
│ ☰   Página principal        │
│                             │
│ Conteúdo                    │
│                             │
└─────────────────────────────┘
```

Quando o usuário abre o menu:

```text
┌──────────────┬──────────────┐
│    MENU      │              │
│              │   Conteúdo   │
│ Componentes  │              │
│ Layouts      │              │
│ Controles    │              │
└──────────────┴──────────────┘
```

---

# 15. Conteúdo das páginas

Para testar a estrutura, foi colocado um conteúdo simples no `Menu`:

```text
Menu
```

E na `MainPage`:

```text
Conteúdo da página inicial
```

Isso permite verificar visualmente se o `FlyoutPage` está funcionando corretamente.

---

# 16. Funcionamento final

A estrutura final do aplicativo funciona da seguinte maneira:

```text
                 App
                  │
                  ▼
             AppFlyOut
                  │
             FlyoutPage
              /       \
             /         \
            ▼           ▼
         Flyout       Detail
           │             │
           ▼             ▼
         Menu      NavigationPage
                         │
                         ▼
                      MainPage
```

Na execução:

1. O aplicativo inicia o `AppFlyOut`.
    
2. O `FlyoutPage` apresenta o menu lateral.
    
3. O `Menu` fica dentro de `Flyout`.
    
4. A `MainPage` fica dentro de `Detail`.
    
5. A `NavigationPage` envolve a `MainPage`.
    
6. O usuário pode abrir e fechar o menu lateral.
    
7. A barra de navegação/título é fornecida pela `NavigationPage`.
    

---

# 17. Resumo dos principais conceitos

|Conceito|Função|
|---|---|
|`Views`|Organiza as páginas do aplicativo|
|`MainPage`|Página principal|
|`Menu`|Conteúdo do menu lateral|
|`FlyoutPage`|Estrutura que permite criar menu lateral|
|`Flyout`|Define a página do menu lateral|
|`Detail`|Define a página principal/conteúdo|
|`NavigationPage`|Adiciona estrutura de navegação e barra de título|
|`AppFlyOut`|Estrutura principal personalizada do aplicativo|
|`FlyoutLayoutBehavior`|Controla o comportamento/apresentação do menu|
|`Popover`|Faz o menu aparecer sobre o conteúdo|
|`App.xaml.cs`|Define a estrutura inicial carregada pelo aplicativo|

---

# 18. Fluxo para memorizar

```text
Criar Views
    ↓
Criar MainPage
    ↓
Criar Menu
    ↓
Criar AppFlyOut
    ↓
Alterar para FlyoutPage
    ↓
Configurar Flyout
    ↓
Configurar Detail
    ↓
Adicionar NavigationPage
    ↓
Definir AppFlyOut como página inicial
    ↓
Configurar comportamento do menu
```

## Ideia principal

A principal mudança desta aula é sair da estrutura padrão baseada em **AppShell** e construir manualmente uma estrutura baseada em **FlyoutPage**.

A arquitetura utilizada será:

```text
App
 ↓
AppFlyOut
 ↓
FlyoutPage
 ├── Flyout → Menu
 │
 └── Detail → NavigationPage → MainPage
```

Essa estrutura servirá como base para as próximas aulas, nas quais serão adicionados os diversos **componentes do .NET MAUI** ao aplicativo Gallery.