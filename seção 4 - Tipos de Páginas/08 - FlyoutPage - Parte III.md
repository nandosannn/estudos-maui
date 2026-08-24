# FlyoutPage no Android e integração com NavigationPage

## 1. Executando o projeto no Android

Nesta aula, o projeto é executado em um dispositivo Android utilizando o modo **Debug**.

O objetivo é observar como o `FlyoutPage`, que foi configurado anteriormente, se comporta em um dispositivo com tela pequena.

No Windows, vimos que o menu lateral pode ficar permanentemente visível ou ser recolhido dependendo da configuração do `FlyoutLayoutBehavior`.

No Android, entretanto, o comportamento é diferente.

---

# 2. O FlyoutPage no Android

Ao executar o aplicativo no Android, o menu lateral continua existindo.

Porém, ele não aparece imediatamente na tela.

Para abrir o menu, o usuário precisa fazer um gesto:

```text
Deslizar da esquerda → para a direita
```

Visualmente:

```text
+--------------------------------+
|                                |
|        Conteúdo                |
|                                |
|                                |
+--------------------------------+

        ↓ deslizar

+----------------+---------------+
| Menu           | Conteúdo      |
|                |               |
| Página 1       |               |
| Página 2       |               |
| Página 3       |               |
+----------------+---------------+
```

Esse comportamento funciona, mas existe um problema de usabilidade.

Muitos usuários não sabem que devem deslizar a tela para abrir o menu.

---

# 3. O problema de usabilidade

Em muitos aplicativos Android, o usuário está acostumado com um botão de menu na parte superior da tela.

Esse botão normalmente é representado pelo ícone de três linhas:

```text
☰
```

Esse ícone é conhecido como **menu hambúrguer**.

O usuário normalmente entende que pode clicar nesse botão para abrir o menu lateral.

O problema é que, utilizando somente o `FlyoutPage`, essa barra superior com o botão de menu não aparece automaticamente da maneira esperada.

Por isso, precisamos adicionar uma outra estrutura:

```text
NavigationPage
```

---

# 4. O papel da NavigationPage

A `NavigationPage` é responsável por fornecer uma estrutura de navegação para a página.

Entre outras coisas, ela fornece uma **barra superior de navegação**, conhecida como toolbar/navigation bar.

Essa barra pode apresentar:

- título da página;
    
- botão para voltar;
    
- botão para abrir o menu do `FlyoutPage`;
    
- outros elementos de navegação.
    

Podemos imaginar a estrutura dessa forma:

```text
+--------------------------------+
| ☰   Página 1                   |
+--------------------------------+
|                                |
|        Conteúdo                |
|                                |
|                                |
+--------------------------------+
```

Agora o usuário pode simplesmente clicar no botão:

```text
☰
```

em vez de precisar descobrir que deve arrastar a tela.

---

# 5. Combinando FlyoutPage e NavigationPage

Aqui está um dos conceitos mais importantes da aula.

Podemos combinar:

```text
FlyoutPage
    +
NavigationPage
```

A estrutura fica aproximadamente assim:

```text
FlyoutPage
│
├── Flyout
│   └── Menu lateral
│
└── Detail
    └── NavigationPage
        └── Página atual
```

Ou seja, o `Detail` não recebe diretamente uma `ContentPage`.

Ele recebe uma `NavigationPage`, que por sua vez contém a página que queremos apresentar.

---

# 6. Por que isso é necessário?

Anteriormente, a navegação era feita assim:

```csharp
flyoutPage.Detail = new Page1();
```

Depois:

```csharp
flyoutPage.Detail = new Page2();
```

E:

```csharp
flyoutPage.Detail = new Page3();
```

O problema é que, dessa maneira, estamos colocando diretamente uma página no `Detail`.

Consequentemente, a `NavigationPage` não existe.

Sem a `NavigationPage`, não temos a barra superior de navegação.

---

# 7. Solução: colocar a página dentro de uma NavigationPage

Em vez de:

```csharp
flyoutPage.Detail = new Page2();
```

passamos a utilizar:

```csharp
flyoutPage.Detail = new NavigationPage(new Page2());
```

Agora a estrutura fica:

```text
FlyoutPage
    ↓
Detail
    ↓
NavigationPage
    ↓
Page2
```

Dessa maneira, a `Page2` fica dentro de uma estrutura de navegação.

---

# 8. NavigationPage utilizando XAML

A aula também apresenta a possibilidade de configurar a `NavigationPage` diretamente no XAML.

A ideia é criar uma `NavigationPage` e informar qual página será colocada dentro dela.

Um exemplo simplificado seria:

```xml
<NavigationPage>
    <x:Arguments>
        <local:Page1 />
    </x:Arguments>
</NavigationPage>
```

O elemento:

```xml
<x:Arguments>
```

é utilizado para fornecer argumentos ao construtor da classe.

Nesse caso, estamos informando que a `NavigationPage` deve receber uma instância de `Page1`.

A estrutura fica:

```text
NavigationPage
      ↓
    Page1
```

---

# 9. O problema ao trocar de página

Existe um detalhe muito importante.

Imagine que inicialmente temos:

```text
FlyoutPage
    ↓
NavigationPage
    ↓
Page1
```

A barra superior aparece corretamente.

Porém, quando o usuário clica em "Página 2", se fizermos:

```csharp
flyoutPage.Detail = new Page2();
```

a estrutura passa a ser:

```text
FlyoutPage
    ↓
Detail
    ↓
Page2
```

A `NavigationPage` desapareceu.

Consequentemente:

```text
❌ Barra superior desaparece
❌ Botão do menu desaparece
```

Por isso, precisamos manter a mesma estrutura durante a navegação.

---

# 10. Corrigindo a navegação

Em vez de colocar diretamente a página no `Detail`, precisamos colocar uma `NavigationPage`.

Então:

```csharp
flyoutPage.Detail = new NavigationPage(new Page2());
```

E para a Página 3:

```csharp
flyoutPage.Detail = new NavigationPage(new Page3());
```

Agora temos:

```text
Página 1:

FlyoutPage
    ↓
NavigationPage
    ↓
Page1
```

Depois:

```text
Página 2:

FlyoutPage
    ↓
NavigationPage
    ↓
Page2
```

E:

```text
Página 3:

FlyoutPage
    ↓
NavigationPage
    ↓
Page3
```

Dessa forma, a barra de navegação continua existindo.

---

# 11. Exemplo completo dos eventos

Podemos adaptar os eventos da aula dessa maneira.

### Página 1

```csharp
private void OnButtonClickedPage1(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new NavigationPage(new Page1());
}
```

### Página 2

```csharp
private void OnButtonClickedPage2(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new NavigationPage(new Page2());
}
```

### Página 3

```csharp
private void OnButtonClickedPage3(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail = new NavigationPage(new Page3());
}
```

A lógica é praticamente a mesma.

A única diferença é a página que será colocada dentro da `NavigationPage`.

---

# 12. Estrutura final da aplicação

Depois das alterações, temos uma estrutura mais completa:

```text
Application
│
└── FlyoutPage
    │
    ├── Flyout
    │   │
    │   ├── Página 1
    │   ├── Página 2
    │   └── Página 3
    │
    └── Detail
        │
        └── NavigationPage
            │
            └── Página atual
```

Essa estrutura permite combinar:

- menu lateral;
    
- navegação;
    
- barra superior;
    
- botão de menu;
    
- botão de voltar;
    
- diferentes páginas como conteúdo.
    

---

# 13. Como o usuário navega

Depois da configuração, o usuário pode clicar no botão de menu.

Por exemplo:

```text
+--------------------------------+
| ☰    Página 1                  |
+--------------------------------+
|                                |
|        Conteúdo da Page1       |
|                                |
+--------------------------------+
```

Ao clicar em:

```text
☰
```

o menu aparece:

```text
+----------------+---------------+
| Página 1       |               |
| Página 2       | Conteúdo      |
| Página 3       |               |
+----------------+---------------+
```

Ao clicar em Página 2:

```text
+--------------------------------+
| ☰    Página 2                  |
+--------------------------------+
|                                |
|        Conteúdo da Page2       |
|                                |
+--------------------------------+
```

E podemos repetir o processo para a Página 3.

---

# 14. FlyoutPage + NavigationPage

É importante diferenciar as responsabilidades.

|Componente|Responsabilidade|
|---|---|
|`FlyoutPage`|Criar a estrutura de menu lateral|
|`Flyout`|Representar o menu|
|`Detail`|Representar o conteúdo principal|
|`NavigationPage`|Fornecer uma estrutura de navegação e barra superior|
|`ContentPage`|Representar uma página de conteúdo|
|`Clicked`|Detectar o clique no item do menu|

Podemos resumir:

```text
FlyoutPage
    │
    ├── Flyout
    │   └── Menu
    │
    └── Detail
        └── NavigationPage
            └── ContentPage
```

---

# 15. Por que essa combinação é interessante?

Em um aplicativo pequeno, talvez não seja necessário utilizar uma estrutura tão completa.

Porém, em aplicativos maiores, podemos ter:

```text
☰ Menu
│
├── Início
├── Usuários
├── Produtos
├── Relatórios
├── Configurações
└── Sobre
```

Cada opção pode apresentar uma página diferente.

Além disso, cada página pode ter sua própria navegação.

Por exemplo:

```text
Usuários
    ↓
Lista de usuários
    ↓
Detalhes do usuário
    ↓
Editar usuário
```

A `NavigationPage` ajuda a estruturar esse tipo de navegação.

---

# 16. Comportamento no Android

No Android, o resultado passa a ser mais familiar para o usuário.

A barra superior pode apresentar um botão semelhante a:

```text
☰
```

O usuário clica nele e abre o menu.

Isso é mais intuitivo do que depender exclusivamente do gesto:

```text
Arrastar da esquerda → direita
```

Portanto, a combinação de `FlyoutPage` com `NavigationPage` proporciona uma experiência mais próxima daquela encontrada em muitos aplicativos móveis.

---

# 17. E o iOS?

A aula também destaca que esse comportamento não é exclusivo do Android.

A solução apresentada também é útil para o **iOS**.

Portanto, ao desenvolver uma aplicação .NET MAUI multiplataforma, essa estrutura pode ser utilizada para fornecer uma experiência de navegação semelhante em diferentes plataformas.

A grande vantagem do .NET MAUI é justamente permitir trabalhar com uma estrutura compartilhada de código para diferentes sistemas.

---

# 18. Exemplo final

Uma implementação simplificada pode ficar assim:

```csharp
private void OnButtonClickedPage1(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail =
        new NavigationPage(new Page1());
}

private void OnButtonClickedPage2(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail =
        new NavigationPage(new Page2());
}

private void OnButtonClickedPage3(object sender, EventArgs e)
{
    var flyoutPage = App.Current.MainPage as FlyoutPage;

    flyoutPage.Detail =
        new NavigationPage(new Page3());
}
```

O ponto fundamental é:

```csharp
flyoutPage.Detail = new NavigationPage(new Page2());
```

e não simplesmente:

```csharp
flyoutPage.Detail = new Page2();
```

Porque, no segundo caso, a `NavigationPage` deixa de existir e, consequentemente, a barra superior de navegação também deixa de existir.

---

# 19. Resumo da aula

Nesta aula aprendemos que o `FlyoutPage` funciona de maneira diferente dependendo do dispositivo.

No Android, o menu lateral pode ser aberto deslizando o dedo da esquerda para a direita.

Porém, depender apenas desse gesto pode não ser a melhor experiência para o usuário.

Para apresentar uma barra superior com um botão de menu, podemos utilizar uma `NavigationPage`.

A estrutura passa a ser:

```text
FlyoutPage
│
├── Flyout
│   └── Menu
│
└── Detail
    └── NavigationPage
        └── Página atual
```

Quando trocamos de página, também precisamos manter a `NavigationPage`.

Por isso, utilizamos:

```csharp
flyoutPage.Detail = new NavigationPage(new Page2());
```

em vez de:

```csharp
flyoutPage.Detail = new Page2();
```

Dessa forma, conseguimos manter a barra superior durante toda a navegação.

---

# 20. Principais conceitos para memorizar

```text
FlyoutPage
    ↓
Possui menu lateral

Flyout
    ↓
Menu lateral

Detail
    ↓
Conteúdo principal

NavigationPage
    ↓
Estrutura de navegação + barra superior

Clicked
    ↓
Evento executado ao clicar em uma opção

App.Current.MainPage
    ↓
Acessa a página principal da aplicação

new NavigationPage(new Page2())
    ↓
Coloca a Page2 dentro de uma estrutura de navegação
```

A ideia central da aula é:

> **O `FlyoutPage` fornece o menu lateral, enquanto a `NavigationPage` pode ser utilizada dentro do `Detail` para fornecer a barra superior e manter a estrutura de navegação durante a troca de páginas.**