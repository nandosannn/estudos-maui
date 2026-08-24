# NavigationPage — Navegação entre páginas e controle da pilha

## 1. Navegação da Página 2 para a Página 3

Depois de aprender a navegar da Página 1 para a Página 2, podemos aplicar o mesmo conceito para navegar da Página 2 para a Página 3.

Para isso, precisamos basicamente de:

1. Um botão na Página 2.
    
2. Um evento `Clicked` associado ao botão.
    
3. O uso da propriedade `Navigation`.
    
4. O método `PushAsync()` para adicionar a Página 3 à pilha de navegação.
    

### Exemplo no XAML

```xml
<Button
    Text="Prosseguir"
    Clicked="OnButtonNextClicked" />
```

No arquivo `.xaml.cs`, podemos implementar o evento:

```csharp
private async void OnButtonNextClicked(object sender, EventArgs e)
{
    await Navigation.PushAsync(new Page3());
}
```

Nesse código:

- `Navigation` representa o sistema de navegação da página.
    
- `PushAsync()` adiciona uma nova página à pilha de navegação.
    
- `new Page3()` cria uma nova instância da Página 3.
    
- `await` aguarda a conclusão da navegação.
    

---

# 2. Renomeando eventos no Visual Studio

Quando utilizamos o atalho `Ctrl + .` sobre o evento no XAML, o Visual Studio pode criar automaticamente o manipulador do evento.

Por exemplo:

```xml
<Button
    Text="Prosseguir"
    Clicked="OnButtonNextClicked" />
```

O método correspondente será:

```csharp
private async void OnButtonNextClicked(object sender, EventArgs e)
{
    
}
```

Caso seja necessário alterar o nome do método, podemos utilizar:

**Ctrl + R, Ctrl + R**

Esse comando permite renomear o método e atualizar automaticamente as referências.

Por exemplo:

```csharp
OnButtonClicked
```

pode ser renomeado para:

```csharp
OnButtonNextClicked
```

O Visual Studio também altera a referência existente no XAML.

---

# 3. Voltando para a página anterior

O `NavigationPage` também permite voltar para a página anterior.

Para isso, utilizamos:

```csharp
await Navigation.PopAsync();
```

Enquanto `PushAsync()` adiciona uma página à pilha, `PopAsync()` remove a página atual da pilha.

Podemos pensar da seguinte maneira:

```text
Página 1
   ↓ PushAsync
Página 1 → Página 2
   ↓ PushAsync
Página 1 → Página 2 → Página 3
```

Se estivermos na Página 3 e executarmos:

```csharp
await Navigation.PopAsync();
```

teremos:

```text
Página 1 → Página 2
```

A Página 3 foi retirada da pilha e voltamos para a Página 2.

---

# 4. Exemplo de botão Voltar

Podemos criar outro botão na Página 2:

```xml
<Button
    Text="Voltar"
    Clicked="OnButtonBackClicked" />
```

E implementar:

```csharp
private async void OnButtonBackClicked(object sender, EventArgs e)
{
    await Navigation.PopAsync();
}
```

É importante lembrar que `PopAsync()` pressupõe que exista uma página anterior na pilha.

Por exemplo, se estamos na Página 2:

```text
Página 1 → Página 2
```

podemos voltar para a Página 1 porque ela existe na pilha.

---

# 5. Navigation Stack

Um dos conceitos mais importantes da aula é o **Navigation Stack**.

A pilha de navegação é responsável por armazenar as páginas que fazem parte do fluxo atual.

Imagine a seguinte sequência:

```text
Página 1
```

Depois:

```text
Página 1 → Página 2
```

Depois:

```text
Página 1 → Página 2 → Página 3
```

Cada chamada de:

```csharp
PushAsync()
```

adiciona uma nova página à pilha.

Podemos visualizar isso como uma pilha:

```text
┌─────────────┐
│   Página 3  │ ← topo
├─────────────┤
│   Página 2  │
├─────────────┤
│   Página 1  │
└─────────────┘
```

Quando utilizamos:

```csharp
PopAsync()
```

a página que está no topo é removida.

```text
┌─────────────┐
│   Página 2  │ ← topo
├─────────────┤
│   Página 1  │
└─────────────┘
```

---

# 6. Acessando o NavigationStack

Podemos acessar a pilha através de:

```csharp
Navigation.NavigationStack
```

Essa propriedade contém as páginas que estão atualmente na pilha de navegação.

Podemos, por exemplo, verificar a quantidade de páginas:

```csharp
int quantidade = Navigation.NavigationStack.Count;
```

Se estivermos na Página 2:

```text
Página 1
Página 2
```

teremos:

```csharp
Navigation.NavigationStack.Count
```

igual a:

```text
2
```

Se estivermos na Página 3:

```text
Página 1
Página 2
Página 3
```

teremos:

```text
3
```

---

# 7. Acessando páginas específicas da pilha

O `NavigationStack` funciona de forma semelhante a uma lista.

Os índices começam em `0`.

Portanto:

|Página|Índice|
|---|--:|
|Página 1|0|
|Página 2|1|
|Página 3|2|

Por exemplo:

```csharp
var pagina2 = Navigation.NavigationStack[1];
```

Nesse caso, estamos acessando a Página 2.

É importante tomar cuidado com os índices. Antes de acessar uma posição, precisamos garantir que ela realmente exista.

---

# 8. Navigation Modal Stack

Além do `NavigationStack`, existe também o:

```csharp
Navigation.ModalStack
```

A navegação modal possui um comportamento diferente da navegação tradicional.

Enquanto o `NavigationStack` é utilizado normalmente para representar um fluxo de páginas:

```text
Página 1 → Página 2 → Página 3
```

o modal geralmente é utilizado para apresentar uma tela temporária sobre a tela atual.

Um exemplo seria:

```text
Página de cadastro
       ↓
Modal com Termos de Uso
```

O usuário visualiza os termos e depois fecha o modal para retornar ao cadastro.

---

# 9. O que é um Modal?

Um modal é uma tela apresentada temporariamente sobre a tela atual.

Um exemplo prático:

```text
┌──────────────────────────────┐
│ Cadastro                     │
│                              │
│ Nome: __________________     │
│                              │
│ [ ] Aceito os termos         │
│                              │
│       Ver termos de uso      │
└──────────────────────────────┘
                ↓
┌──────────────────────────────┐
│ Termos de Uso                │
│                              │
│ Texto dos termos...          │
│                              │
│            [Fechar]          │
└──────────────────────────────┘
```

O modal pode ser utilizado para:

- Termos de uso;
    
- Confirmações;
    
- Formulários temporários;
    
- Informações complementares;
    
- Seleção de opções;
    
- Outras telas que não fazem necessariamente parte do fluxo principal.
    

O modal não precisa ter uma aparência específica. A interface pode ser construída de acordo com a necessidade do aplicativo.

---

# 10. PushAsync() e PushModalAsync()

Existem dois métodos diferentes para adicionar páginas.

### Navegação normal

```csharp
await Navigation.PushAsync(new Page3());
```

Utilizamos quando queremos adicionar uma página à pilha de navegação tradicional.

### Navegação modal

```csharp
await Navigation.PushModalAsync(new ModalPage());
```

Utilizamos quando queremos apresentar uma página como modal.

Podemos visualizar:

```text
PushAsync()
    ↓
NavigationStack
```

e:

```text
PushModalAsync()
    ↓
ModalStack
```

---

# 11. PopAsync()

O método:

```csharp
await Navigation.PopAsync();
```

remove a página atual da pilha de navegação normal.

Exemplo:

```text
Página 1 → Página 2 → Página 3
```

Depois de:

```csharp
await Navigation.PopAsync();
```

ficamos com:

```text
Página 1 → Página 2
```

Portanto:

**PushAsync() = adiciona uma página**

**PopAsync() = remove a página atual**

---

# 12. PopModalAsync()

Para fechar um modal, utilizamos:

```csharp
await Navigation.PopModalAsync();
```

Esse método deve ser utilizado quando estamos trabalhando com uma página modal.

Exemplo:

```text
Cadastro
   ↓
Modal de Termos
```

Ao executar:

```csharp
await Navigation.PopModalAsync();
```

o modal é fechado e voltamos para a tela anterior.

Portanto:

```text
PopAsync()
    → remove uma página normal

PopModalAsync()
    → fecha/remove o modal atual
```

---

# 13. PopToRootAsync()

Outro método importante é:

```csharp
await Navigation.PopToRootAsync();
```

Ele serve para voltar diretamente para a primeira página da pilha.

Imagine:

```text
Página 1 → Página 2 → Página 3
```

Se estivermos na Página 3 e executarmos:

```csharp
await Navigation.PopToRootAsync();
```

o resultado será:

```text
Página 1
```

As páginas intermediárias são removidas da pilha.

Isso é útil quando temos um fluxo com várias etapas.

Por exemplo:

```text
Etapa 1 → Etapa 2 → Etapa 3 → Etapa 4
```

Depois de finalizar o cadastro, podemos voltar diretamente para o início:

```csharp
await Navigation.PopToRootAsync();
```

Em vez de fazer:

```csharp
await Navigation.PopAsync();
await Navigation.PopAsync();
await Navigation.PopAsync();
```

---

# 14. RemovePage()

Também podemos remover uma página específica da pilha utilizando:

```csharp
Navigation.RemovePage(page);
```

Imagine:

```text
Página 1 → Página 2 → Página 3
```

Estamos na Página 3, mas queremos remover especificamente a Página 2.

Podemos obter a Página 2 através do `NavigationStack`:

```csharp
var pagina2 = Navigation.NavigationStack[1];
```

Depois:

```csharp
Navigation.RemovePage(pagina2);
```

A pilha passa a ser:

```text
Página 1 → Página 3
```

Agora, se executarmos:

```csharp
await Navigation.PopAsync();
```

voltaremos diretamente para a Página 1.

---

# 15. InsertPageBefore()

Também podemos inserir uma página em uma posição específica da pilha.

Para isso, utilizamos:

```csharp
Navigation.InsertPageBefore(pagina, antesDaPagina);
```

Imagine:

```text
Página 1 → Página 2 → Página 3
```

Queremos inserir a Página 4 antes da Página 3.

Podemos fazer:

```csharp
Navigation.InsertPageBefore(
    new Page4(),
    Navigation.NavigationStack[2]
);
```

O resultado será:

```text
Página 1 → Página 2 → Página 4 → Página 3
```

O primeiro parâmetro representa a página que será inserida.

O segundo representa a página antes da qual ela será colocada.

---

# 16. Principais métodos de navegação

Podemos resumir os principais métodos apresentados na aula:

|Método|Função|
|---|---|
|`PushAsync()`|Adiciona uma página à pilha normal|
|`PopAsync()`|Remove a página atual e volta para a anterior|
|`PushModalAsync()`|Abre uma página como modal|
|`PopModalAsync()`|Fecha o modal atual|
|`PopToRootAsync()`|Volta diretamente para a primeira página|
|`RemovePage()`|Remove uma página específica da pilha|
|`InsertPageBefore()`|Insere uma página antes de outra página|
|`NavigationStack`|Permite acessar a pilha de páginas normais|
|`ModalStack`|Permite acessar a pilha de páginas modais|

---

# 17. Fluxo completo da navegação

Um fluxo simples pode ser representado assim:

```text
Página 1
   │
   │ PushAsync()
   ↓
Página 2
   │
   │ PushAsync()
   ↓
Página 3
```

Na Página 3:

```csharp
await Navigation.PopAsync();
```

Resultado:

```text
Página 1
   │
   ↓
Página 2
```

Se utilizarmos:

```csharp
await Navigation.PopToRootAsync();
```

resultado:

```text
Página 1
```

---

# 18. Exemplo completo

### Página 2 — XAML

```xml
<VerticalStackLayout
    Padding="30"
    Spacing="20"
    VerticalOptions="Center">

    <Button
        Text="Prosseguir"
        Clicked="OnButtonNextClicked" />

    <Button
        Text="Voltar"
        Clicked="OnButtonBackClicked" />

</VerticalStackLayout>
```

### Página 2 — Code Behind

```csharp
public partial class Page2 : ContentPage
{
    public Page2()
    {
        InitializeComponent();
    }

    private async void OnButtonNextClicked(object sender, EventArgs e)
    {
        await Navigation.PushAsync(new Page3());
    }

    private async void OnButtonBackClicked(object sender, EventArgs e)
    {
        await Navigation.PopAsync();
    }
}
```

Nesse exemplo:

- O botão **Prosseguir** chama a Página 3.
    
- O botão **Voltar** remove a Página 2 da pilha e retorna para a página anterior.
    
- `PushAsync()` é utilizado para avançar.
    
- `PopAsync()` é utilizado para voltar.
    

---

# 19. Conceito principal da aula

O principal conceito desta aula é entender que o `NavigationPage` trabalha com uma **pilha de páginas**.

Quando avançamos:

```csharp
PushAsync()
```

uma página é colocada no topo da pilha.

Quando voltamos:

```csharp
PopAsync()
```

a página que está no topo é removida.

Podemos imaginar:

```text
PushAsync()
     ↓
┌──────────┐
│ Página 3 │ ← adicionada
├──────────┤
│ Página 2 │
├──────────┤
│ Página 1 │
└──────────┘
```

E:

```text
PopAsync()
     ↓
┌──────────┐
│ Página 2 │ ← volta para cá
├──────────┤
│ Página 1 │
└──────────┘
```

Dessa forma, o sistema consegue controlar o histórico de navegação do aplicativo.

---

# 20. Resumo

Nesta aula foram apresentados os principais recursos de navegação do `NavigationPage`.

Aprendi que:

- `PushAsync()` adiciona uma nova página à pilha.
    
- `PopAsync()` remove a página atual e volta para a anterior.
    
- `PushModalAsync()` abre uma página modal.
    
- `PopModalAsync()` fecha o modal atual.
    
- `PopToRootAsync()` retorna diretamente para a primeira página.
    
- `NavigationStack` armazena as páginas da navegação normal.
    
- `ModalStack` armazena as páginas modais.
    
- `RemovePage()` permite remover uma página específica da pilha.
    
- `InsertPageBefore()` permite inserir uma página antes de outra.
    
- Os índices do `NavigationStack` começam em `0`.
    
- A navegação normal é organizada como uma pilha.
    
- O modal possui um fluxo diferente da navegação tradicional e é indicado para telas temporárias, como termos de uso ou confirmações.
    

A ideia central é:

```text
PushAsync()       → avançar
PopAsync()        → voltar
PopToRootAsync()  → voltar para o início
PushModalAsync()  → abrir modal
PopModalAsync()   → fechar modal
```