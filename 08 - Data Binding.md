
# Índice

- [[#1. O que é Data Binding]]
- [[#2. Binding de Propriedades]]
- [[#3. BindingContext]]
- [[#4. Modos de Binding]]
    - [[#4.1 OneWay]]
    - [[#4.2 TwoWay]]
    - [[#4.3 OneTime]]
    - [[#4.4 OneWayToSource]]
- [[#5. Binding entre Controles]]
- [[#6. Binding de Objetos]]
- [[#7. Binding de Listas]]
- [[#8. INotifyPropertyChanged]]
- [[#9. ObservableCollection]]
- [[#10. Command e ICommand]]
- [[#11. Relação entre os Conceitos]]
- [[#12. Tabela-Resumo]]

---

# 1. O que é Data Binding

**Data Binding** é o mecanismo que permite **ligar uma propriedade de um elemento da interface a uma propriedade de um objeto**.

Em vez de alterar manualmente a interface através do código, podemos estabelecer uma ligação:

```
Objeto / ViewModel
       │
       │ Data Binding
       ▼
Interface XAML
```

Por exemplo:

```
public class Pessoa
{
    public string Nome { get; set; }
}
```

No XAML:

```
<Label Text="{Binding Nome}" />
```

Se o `BindingContext` do `Label` for um objeto `Pessoa`, o `Label` buscará automaticamente o valor da propriedade `Nome`.

Se:

```
Pessoa pessoa = new Pessoa
{
    Nome = "Fernando"
};
```

Então:

```
<Label Text="{Binding Nome}" />
```

exibirá:

```
Fernando
```

### Sem Data Binding

Seria necessário fazer manualmente:

```
label.Text = pessoa.Nome;
```

### Com Data Binding

```
<Label Text="{Binding Nome}" />
```

O XAML declara **de onde o valor deve vir**.

---

# 2. Binding de Propriedades

O binding normalmente conecta:

```
Propriedade da View
        ↓
Propriedade do objeto
```

Exemplo:

```
<Entry Text="{Binding Nome}" />
```

Aqui temos:

```
Entry.Text
    │
    │ Binding
    ▼
Pessoa.Nome
```

O `Text` do `Entry` está ligado à propriedade `Nome`.

Outro exemplo:

```
<Label Text="{Binding Nome}" />
```

---

## Exemplo completo

Classe:

```
public class Pessoa
{
    public string Nome { get; set; }
    public int Idade { get; set; }
}
```

XAML:

```
<VerticalStackLayout>

    <Label Text="{Binding Nome}" />

    <Label Text="{Binding Idade}" />

</VerticalStackLayout>
```

Código:

```
BindingContext = new Pessoa
{
    Nome = "Fernando",
    Idade = 27
};
```

Resultado:

```
Fernando
27
```

---

# 3. BindingContext

O **`BindingContext` define o objeto que será utilizado como fonte dos bindings**.

Imagine:

```
<Label Text="{Binding Nome}" />
```

A pergunta é:

> De onde vem `Nome`?

A resposta está no:

```
BindingContext
```

Por exemplo:

```
BindingContext = new Pessoa
{
    Nome = "Fernando"
};
```

Agora:

```
<Label Text="{Binding Nome}" />
```

significa:

```
BindingContext.Nome
```

ou seja:

```
Pessoa.Nome
```

### Visualmente

```
BindingContext
     │
     ▼
 Pessoa
 ┌──────────────┐
 │ Nome         │
 │ Idade        │
 └──────────────┘
     │
     │ Binding
     ▼
   Label
```

---

## BindingContext pode ser herdado

Um ponto importante no MAUI:

**Elementos visuais normalmente herdam o `BindingContext` de seus elementos-pai.**

Por exemplo:

```
<VerticalStackLayout>

    <Label Text="{Binding Nome}" />

    <Entry Text="{Binding Nome}" />

</VerticalStackLayout>
```

Se o `VerticalStackLayout` possui:

```
BindingContext = pessoa;
```

seus filhos podem utilizar:

```
Nome
```

sem precisar definir o `BindingContext` individualmente.

---

# 4. Modos de Binding

O MAUI possui diferentes formas de determinar **a direção da comunicação entre a View e a fonte de dados**.

Os principais modos são:

```
OneWay
TwoWay
OneTime
OneWayToSource
```

---

# 4.1 OneWay

No `OneWay`, a informação vai:

```
Fonte → Interface
```

Exemplo:

```
<Label Text="{Binding Nome, Mode=OneWay}" />
```

Se:

```
Pessoa.Nome = "Fernando";
```

o `Label` recebe:

```
Fernando
```

Mas alterações feitas no `Label` não atualizam a propriedade da fonte.

### Fluxo

```
Pessoa.Nome
    │
    ▼
 Label.Text
```

É bastante utilizado quando a interface **apenas exibe informações**.

Exemplo:

```
<Label Text="{Binding Nome}" />
```

---

# 4.2 TwoWay

No `TwoWay`, a comunicação ocorre nos dois sentidos:

```
Fonte ⇄ Interface
```

Exemplo:

```
<Entry Text="{Binding Nome, Mode=TwoWay}" />
```

Se o objeto tiver:

```
Nome = "Fernando";
```

o `Entry` exibirá:

```
Fernando
```

Se o usuário alterar o texto para:

```
João
```

a propriedade:

```
Nome
```

também poderá ser atualizada.

### Fluxo

```
Pessoa.Nome
    ⇅
Entry.Text
```

É muito comum em **formulários**.

```
<Entry Placeholder="Nome"
       Text="{Binding Nome, Mode=TwoWay}" />
```

---

# 4.3 OneTime

No `OneTime`, o valor é obtido **uma vez**, durante a criação do binding.

```
<Label Text="{Binding Nome, Mode=OneTime}" />
```

O valor inicial é obtido da fonte.

Depois disso, alterações posteriores na propriedade da fonte não são utilizadas para atualizar automaticamente a interface.

### Fluxo

```
Fonte ──────→ Interface
       uma vez
```

É útil quando o valor **não precisa ser atualizado depois da inicialização**.

---

# 4.4 OneWayToSource

É o sentido inverso do `OneWay`:

```
Interface → Fonte
```

Exemplo conceitual:

```
<Entry Text="{Binding Nome, Mode=OneWayToSource}" />
```

O valor da interface é enviado para a propriedade da fonte.

### Fluxo

```
Entry.Text
    │
    ▼
Pessoa.Nome
```

É menos utilizado que `OneWay` e `TwoWay`, mas é importante conhecer para provas.

---

# 5. Binding entre Controles

O Data Binding também pode conectar **um controle diretamente a outro controle**.

Por exemplo, imagine:

```
<Slider x:Name="slider"
        Minimum="0"
        Maximum="100" />

<Label Text="{Binding Source={x:Reference slider},
                      Path=Value}" />
```

O `Label` está ligado ao `Value` do `Slider`.

```
Slider.Value
      │
      ▼
Label.Text
```

Se o usuário movimentar o `Slider`, o `Label` pode acompanhar o valor.

### Conceito importante

Nesse caso, não estamos necessariamente usando um objeto como fonte.

Estamos fazendo:

```
Controle → Controle
```

O:

```
x:Reference
```

permite referenciar outro elemento XAML pelo nome.

---

# 6. Binding de Objetos

Podemos utilizar Data Binding com objetos complexos.

Imagine:

```
public class Pessoa
{
    public string Nome { get; set; }

    public Endereco Endereco { get; set; }
}

public class Endereco
{
    public string Cidade { get; set; }
}
```

Podemos fazer:

```
<Label Text="{Binding Nome}" />

<Label Text="{Binding Endereco.Cidade}" />
```

Se:

```
Pessoa pessoa = new Pessoa
{
    Nome = "Fernando",
    Endereco = new Endereco
    {
        Cidade = "Natal"
    }
};
```

teremos:

```
Nome → Fernando
Cidade → Natal
```

### Binding aninhado

```
Pessoa
 ├── Nome
 │
 └── Endereco
       └── Cidade
```

No XAML:

```
{Binding Endereco.Cidade}
```

---

# 7. Binding de Listas

Data Binding também pode trabalhar com **coleções**.

Imagine:

```
public class Pessoa
{
    public string Nome { get; set; }
}
```

E:

```
public List<Pessoa> Pessoas { get; set; }
```

Podemos utilizar um controle como:

```
<CollectionView ItemsSource="{Binding Pessoas}">
    
    <CollectionView.ItemTemplate>
        <DataTemplate>
            <Label Text="{Binding Nome}" />
        </DataTemplate>
    </CollectionView.ItemTemplate>

</CollectionView>
```

Aqui temos dois níveis de binding.

### Primeiro

```
ItemsSource="{Binding Pessoas}"
```

Busca a lista:

```
ViewModel
   │
   ▼
Pessoas
   │
   ▼
CollectionView
```

### Segundo

Dentro do `DataTemplate`:

```
<Label Text="{Binding Nome}" />
```

Nesse contexto, o `BindingContext` representa **cada elemento da lista**.

```
Pessoas
 │
 ├── Pessoa 1 → Nome
 ├── Pessoa 2 → Nome
 └── Pessoa 3 → Nome
```

---

# 8. INotifyPropertyChanged

Aqui está um dos conceitos **mais importantes** de Data Binding em .NET MAUI.

Imagine:

```
public class Pessoa
{
    public string Nome { get; set; }
}
```

Inicialmente:

```
Nome = "Fernando"
```

A interface mostra:

```
Fernando
```

Agora fazemos:

```
pessoa.Nome = "João";
```

Será que o `Label` necessariamente saberá que `Nome` mudou?

**Não.**

Precisamos de um mecanismo para notificar a interface.

É aí que entra:

```
INotifyPropertyChanged
```

Ele permite que um objeto informe:

> "Uma das minhas propriedades mudou."

---

## Exemplo

```
using System.ComponentModel;

public class Pessoa : INotifyPropertyChanged
{
    private string nome;

    public string Nome
    {
        get => nome;

        set
        {
            if (nome != value)
            {
                nome = value;

                PropertyChanged?.Invoke(
                    this,
                    new PropertyChangedEventArgs(nameof(Nome))
                );
            }
        }
    }

    public event PropertyChangedEventHandler PropertyChanged;
}
```

Agora, quando fazemos:

```
pessoa.Nome = "João";
```

o objeto dispara uma notificação:

```
Nome mudou!
```

O Binding recebe essa informação e pode atualizar a interface.

### Fluxo

```
pessoa.Nome = "João"
          │
          ▼
INotifyPropertyChanged
          │
          ▼
   Binding percebe
          │
          ▼
      Label.Text
```

---

# 9. ObservableCollection

Agora temos outro problema.

Imagine:

```
List<Pessoa> Pessoas
```

Se adicionarmos uma pessoa:

```
Pessoas.Add(novaPessoa);
```

a interface pode não saber que a lista foi modificada.

Para isso existe:

```
ObservableCollection<T>
```

Ela notifica alterações estruturais na coleção.

Exemplo:

```
using System.Collections.ObjectModel;

public ObservableCollection<Pessoa> Pessoas { get; set; }
```

Inicialização:

```
Pessoas = new ObservableCollection<Pessoa>();
```

Adicionando:

```
Pessoas.Add(new Pessoa
{
    Nome = "Fernando"
});
```

A coleção notifica que um elemento foi adicionado.

---

## List vs ObservableCollection

|`List<T>`|`ObservableCollection<T>`|
|---|---|
|Coleção comum|Coleção observável|
|Não notifica automaticamente alterações|Notifica alterações|
|`Add()` não comunica a UI|`Add()` pode atualizar a UI via binding|
|Útil para dados estáticos|Muito útil para listas dinâmicas na UI|

### Atenção

`ObservableCollection` resolve **alterações na coleção**:

```
Adicionar
Remover
Mover
etc.
```

Ela não substitui `INotifyPropertyChanged` para alterações **nas propriedades dos elementos**.

Por exemplo:

```
Pessoas[0].Nome = "João";
```

Para a UI acompanhar essa alteração, o objeto `Pessoa` deve implementar adequadamente `INotifyPropertyChanged`.

---

# 10. Command e ICommand

Data Binding não serve apenas para dados.

Ele também pode ser utilizado para **ações**.

Em MAUI, é comum utilizar:

```
Command
ICommand
```

para conectar uma ação da interface a um método do ViewModel.

Por exemplo:

```
<Button Text="Salvar"
        Command="{Binding SalvarCommand}" />
```

O botão está ligado a:

```
SalvarCommand
```

---

## ICommand

`ICommand` é uma **interface** que representa uma ação que pode ser executada.

Ela possui principalmente:

```
Execute()
```

e:

```
CanExecute()
```

Conceitualmente:

```
Button
  │
  │ Command Binding
  ▼
ICommand
  │
  ├── CanExecute()
  │
  └── Execute()
```

---

## Command

`Command` é uma implementação prática de `ICommand`.

Exemplo:

```
public ICommand SalvarCommand { get; }

public MinhaViewModel()
{
    SalvarCommand = new Command(Salvar);
}

private void Salvar()
{
    // lógica para salvar
}
```

No XAML:

```
<Button Text="Salvar"
        Command="{Binding SalvarCommand}" />
```

Agora:

```
Usuário clica no botão
          ↓
      Command
          ↓
       Salvar()
```

Isso evita colocar toda a lógica diretamente no `code-behind`.

---

# 11. Relação entre os Conceitos

Esses conceitos fazem parte de um mesmo mecanismo.

Imagine um aplicativo com cadastro de pessoas:

```
                  ViewModel
                     │
       ┌─────────────┼──────────────┐
       │             │              │
       ▼             ▼              ▼
    Pessoa        Pessoas      SalvarCommand
       │             │              │
       │             │              │
       ▼             ▼              ▼
INotifyProperty   Observable       ICommand
   Changed        Collection
       │             │              │
       └─────────────┼──────────────┘
                     │
                     ▼
                  Binding
                     │
                     ▼
                    XAML
```

### Exemplo

ViewModel:

```
public class PessoaViewModel
{
    public Pessoa Pessoa { get; set; }

    public ObservableCollection<Pessoa> Pessoas { get; set; }

    public ICommand SalvarCommand { get; }
}
```

XAML:

```
<Entry Text="{Binding Pessoa.Nome}" />

<Button Text="Salvar"
        Command="{Binding SalvarCommand}" />

<CollectionView ItemsSource="{Binding Pessoas}">
    <CollectionView.ItemTemplate>
        <DataTemplate>
            <Label Text="{Binding Nome}" />
        </DataTemplate>
    </CollectionView.ItemTemplate>
</CollectionView>
```

Temos então:

```
Entry
 │
 │ TwoWay Binding
 ▼
Pessoa.Nome

Button
 │
 │ Command Binding
 ▼
SalvarCommand

CollectionView
 │
 │ ItemsSource
 ▼
ObservableCollection<Pessoa>
```

---

# 12. Tabela-Resumo

|Conceito|O que é|Fluxo/Finalidade|Exemplo|
|---|---|---|---|
|**Data Binding**|Ligação entre dados e interface|Sincronizar View ↔ dados|`{Binding Nome}`|
|**Binding de propriedades**|Liga uma propriedade da View a uma propriedade de dados|Exibir/alterar valores|`Text="{Binding Nome}"`|
|**`BindingContext`**|Define a fonte dos bindings|Indica de onde vêm os dados|`BindingContext = pessoa`|
|**`OneWay`**|Dados vão da fonte para a View|Exibição|`Label.Text`|
|**`TwoWay`**|Dados vão nos dois sentidos|Formulários/edição|`Entry.Text`|
|**`OneTime`**|Obtém o valor uma única vez|Dados que não precisam acompanhar mudanças|`{Binding Nome, Mode=OneTime}`|
|**`OneWayToSource`**|View envia dados para a fonte|Atualização somente da fonte|`Entry → ViewModel`|
|**Binding entre controles**|Liga propriedades de controles|Comunicação entre elementos XAML|`Slider.Value → Label.Text`|
|**Binding de objetos**|Acessa propriedades de objetos|Trabalhar com objetos complexos|`{Binding Endereco.Cidade}`|
|**Binding de listas**|Liga coleções a controles|Exibir listas|`ItemsSource="{Binding Pessoas}"`|
|**`INotifyPropertyChanged`**|Notifica alteração de propriedades|Atualizar UI quando uma propriedade muda|`Nome` mudou|
|**`ObservableCollection<T>`**|Coleção que notifica alterações|Atualizar UI quando itens são adicionados/removidos|`Pessoas.Add(...)`|
|**`ICommand`**|Contrato para representar ações|Executar comandos através do Binding|`Command="{Binding SalvarCommand}"`|
|**`Command`**|Implementação de `ICommand`|Associar método a ações da UI|`new Command(Salvar)`|

---

# 🎯 O que mais cai / o que você precisa memorizar

### 1. `BindingContext`

> **Define a fonte dos dados que o `{Binding ...}` irá consultar.**

```
BindingContext = pessoa;
```

```
<Label Text="{Binding Nome}" />
```

---

### 2. Modos de Binding

Memorize a direção:

```
OneWay
Fonte ─────────→ View


TwoWay
Fonte ⇄ View


OneTime
Fonte ─────→ View
       uma vez


OneWayToSource
Fonte ←──────── View
```

---

### 3. `INotifyPropertyChanged`

> **Notifica que uma propriedade de um objeto foi alterada.**

```
Pessoa.Nome mudou
       ↓
PropertyChanged
       ↓
Binding
       ↓
UI atualizada
```

---

### 4. `ObservableCollection`

> **Notifica alterações na coleção.**

```
Pessoas.Add(pessoa);
```

```
ObservableCollection
        ↓
Notificação
        ↓
CollectionView
        ↓
UI atualizada
```

---

### 5. `ICommand` / `Command`

> **Permitem representar ações como propriedades que podem ser vinculadas à interface.**

```
<Button Command="{Binding SalvarCommand}" />
```

```
Clique
  ↓
Command
  ↓
Execute()
  ↓
Método
```

---

## 🧠 Mapa mental final

```
                     DATA BINDING
                          │
         ┌────────────────┼────────────────┐
         │                │                │
         ▼                ▼                ▼
     PROPRIEDADES      OBJETOS           LISTAS
         │                │                │
         ▼                ▼                ▼
      Binding         Pessoa           Observable
      Context         Endereco          Collection
         │
         ▼
      DIREÇÃO
         │
   ┌─────┼──────┬────────────┐
   ▼     ▼      ▼            ▼
OneWay TwoWay OneTime OneWayToSource
         │
         ▼
    NOTIFICAÇÕES
      │       │
      ▼       ▼
INotifyProperty  Observable
Changed          Collection
      │
      └───────┐
              ▼
             UI
              │
              ▼
          INTERAÇÃO
              │
              ▼
        ICommand / Command
```

**Regra de ouro para provas:** `INotifyPropertyChanged` está relacionado à **mudança de propriedades**; `ObservableCollection` está relacionada à **mudança de itens da coleção**; e `ICommand` está relacionado à **execução de ações**.