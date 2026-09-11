# Componentes básicos do .NET MAUI

No **.NET MAUI**, os componentes visuais são chamados de **Controls**. Eles são usados para construir a interface da aplicação e permitem que o usuário **visualize informações, digite dados, faça escolhas e execute ações**.

A maioria desses componentes é declarada no **XAML**, enquanto seu comportamento pode ser controlado pelo **C#**.

---

## 1. `Label`

O `Label` é utilizado para **exibir textos** na interface.

```
<Label
    Text="Olá, mundo!"
    FontSize="24"
    HorizontalOptions="Center" />
```

### Principais propriedades

|Propriedade|Função|
|---|---|
|`Text`|Texto exibido|
|`FontSize`|Tamanho da fonte|
|`TextColor`|Cor do texto|
|`FontAttributes`|Negrito, itálico etc.|
|`HorizontalOptions`|Alinhamento horizontal|
|`VerticalOptions`|Alinhamento vertical|
|`HorizontalTextAlignment`|Alinhamento do texto|

### Exemplo

```
<Label
    Text="Número da Sorte"
    FontSize="30"
    FontAttributes="Bold" />
```

**Uso:** títulos, descrições, mensagens, resultados etc.

---

# 2. `Button`

O `Button` representa um **botão que pode executar uma ação**.

```
<Button
    Text="Calcular"
    Clicked="OnCalcularClicked" />
```

No C#:

```
private void OnCalcularClicked(object sender, EventArgs e)
{
    DisplayAlert("Aviso", "Botão clicado!", "OK");
}
```

### Principais propriedades

|Propriedade|Função|
|---|---|
|`Text`|Texto do botão|
|`Clicked`|Evento disparado ao clicar|
|`IsEnabled`|Habilita/desabilita|
|`BackgroundColor`|Cor de fundo|
|`TextColor`|Cor do texto|
|`ImageSource`|Imagem/ícone do botão|

**Uso:** salvar, excluir, calcular, enviar, navegar etc.

---

# 3. `Image`

O `Image` é utilizado para **exibir imagens**.

```
<Image
    Source="logo.png"
    HeightRequest="100"
    WidthRequest="100" />
```

A imagem pode estar, por exemplo, na pasta:

```
Resources/
└── Images/
    └── logo.png
```

### Principais propriedades

|Propriedade|Função|
|---|---|
|`Source`|Define a imagem|
|`HeightRequest`|Altura|
|`WidthRequest`|Largura|
|`Aspect`|Como a imagem será ajustada|
|`IsVisible`|Define se está visível|

### `Aspect`

```
<Image Source="foto.png" Aspect="AspectFit" />
```

Alguns modos:

- `AspectFit` → mantém a proporção e cabe dentro do espaço.
- `AspectFill` → preenche o espaço, podendo cortar partes.
- `Fill` → ocupa todo o espaço, podendo distorcer.

---

# 4. `Entry`

O `Entry` é utilizado para **entrada de texto em uma única linha**.

```
<Entry
    Placeholder="Digite seu nome" />
```

Por exemplo:

```
<Entry
    x:Name="NomeEntry"
    Placeholder="Nome" />
```

No C#:

```
string nome = NomeEntry.Text;
```

### Principais propriedades

|Propriedade|Função|
|---|---|
|`Text`|Valor digitado|
|`Placeholder`|Texto de orientação|
|`Keyboard`|Tipo de teclado|
|`IsPassword`|Oculta o texto|
|`MaxLength`|Limita caracteres|

### Exemplos

Campo de senha:

```
<Entry
    Placeholder="Senha"
    IsPassword="True" />
```

Campo numérico:

```
<Entry
    Keyboard="Numeric"
    Placeholder="Idade" />
```

**Uso:** nome, CPF, e-mail, senha, telefone etc.

---

# 5. `Editor`

O `Editor` também permite entrada de texto, mas é destinado a **textos maiores e multilinha**.

```
<Editor
    Placeholder="Digite sua mensagem..."
    HeightRequest="150" />
```

### Diferença entre `Entry` e `Editor`

|`Entry`|`Editor`|
|---|---|
|Uma linha|Várias linhas|
|Texto curto|Texto longo|
|Nome|Comentário|
|E-mail|Descrição|
|Senha|Mensagem|

**Regra simples:**

> `Entry` → texto curto/uma linha  
> `Editor` → texto longo/várias linhas

---

# 6. `CheckBox`

O `CheckBox` permite selecionar ou desmarcar uma opção.

```
<CheckBox
    x:Name="AceiteCheckBox" />
```

Seu estado pode ser obtido através da propriedade `IsChecked`.

```
bool aceitou = AceiteCheckBox.IsChecked;
```

Também podemos colocar um `Label` ao lado:

```
<HorizontalStackLayout>
    <CheckBox />
    <Label
        Text="Aceito os termos de uso"
        VerticalOptions="Center" />
</HorizontalStackLayout>
```

### Estados

```
☐ Não selecionado

☑ Selecionado
```

**Uso:** termos de uso, preferências, múltiplas opções independentes etc.

---

# 7. `RadioButton`

O `RadioButton` é usado quando o usuário precisa escolher **uma opção entre várias**.

```
<VerticalStackLayout>

    <RadioButton
        Content="Masculino"
        GroupName="Sexo" />

    <RadioButton
        Content="Feminino"
        GroupName="Sexo" />

</VerticalStackLayout>
```

O `GroupName` permite determinar quais opções pertencem ao mesmo grupo.

### Conceito importante

Se temos:

```
( ) Masculino
( ) Feminino
( ) Outro
```

normalmente o usuário pode selecionar **apenas uma opção**.

### Diferença

|CheckBox|RadioButton|
|---|---|
|Pode selecionar várias|Normalmente uma opção|
|Opções independentes|Opções mutuamente exclusivas|
|☐|◉|

---

# 8. `Switch`

O `Switch` representa uma opção **ligada/desligada**.

```
<Switch
    x:Name="NotificacoesSwitch" />
```

Seu estado é obtido através de:

```
bool ativo = NotificacoesSwitch.IsToggled;
```

Visualmente:

```
OFF  → desligado

ON   → ligado
```

Exemplo:

```
<HorizontalStackLayout>
    <Label
        Text="Receber notificações" />

    <Switch />
</HorizontalStackLayout>
```

**Uso:** ativar notificações, modo escuro, localização, configurações etc.

---

# 9. `Slider`

O `Slider` permite selecionar um **valor dentro de um intervalo**, arrastando um controle.

```
<Slider
    Minimum="0"
    Maximum="100"
    Value="50" />
```

Nesse exemplo:

```
0 ----------------●---------------- 100
                  50
```

### Principais propriedades

|Propriedade|Função|
|---|---|
|`Minimum`|Valor mínimo|
|`Maximum`|Valor máximo|
|`Value`|Valor atual|
|`MinimumTrackColor`|Cor da parte preenchida|
|`MaximumTrackColor`|Cor da parte restante|

Podemos acompanhar o valor:

```
<Slider
    ValueChanged="OnSliderValueChanged" />
```

**Uso:** volume, brilho, porcentagem, intensidade etc.

---

# 10. `Picker`

O `Picker` permite que o usuário **escolha uma opção de uma lista**.

```
<Picker
    Title="Selecione uma cidade">
    
    <Picker.Items>
        <x:String>Natal</x:String>
        <x:String>Recife</x:String>
        <x:String>João Pessoa</x:String>
    </Picker.Items>

</Picker>
```

Visualmente, temos algo semelhante a:

```
┌───────────────────────┐
│ Selecione uma cidade ▼│
└───────────────────────┘
```

Também podemos preencher através do C#:

```
CidadePicker.Items.Add("Natal");
CidadePicker.Items.Add("Recife");
CidadePicker.Items.Add("Fortaleza");
```

**Uso:** estado, cidade, categoria, profissão, tipo de usuário etc.

---

# 11. `DatePicker`

O `DatePicker` permite que o usuário **selecione uma data**.

```
<DatePicker
    x:Name="DataPicker" />
```

Podemos definir uma data inicial:

```
<DatePicker
    Date="2026-08-31" />
```

No C#:

```
DateTime data = DataPicker.Date;
```

### Exemplo

```
<VerticalStackLayout>

    <Label Text="Data de nascimento" />

    <DatePicker
        x:Name="DataNascimentoPicker" />

</VerticalStackLayout>
```

**Uso:** nascimento, agendamento, vencimento, início/fim de eventos etc.

---

# 12. `TimePicker`

O `TimePicker` permite selecionar um **horário**.

```
<TimePicker
    x:Name="HorarioPicker" />
```

Podemos definir um horário inicial:

```
<TimePicker
    Time="08:00:00" />
```

No C#:

```
TimeSpan horario = HorarioPicker.Time;
```

**Uso:** horário de entrada, saída, alarmes, agendamentos etc.

---

# 🧠 Quadro-resumo

|Componente|Finalidade|Exemplo|
|---|---|---|
|`Label`|Exibir texto|Título|
|`Button`|Executar ação|Salvar|
|`Image`|Exibir imagem|Logo|
|`Entry`|Entrada de texto curto|Nome|
|`Editor`|Entrada de texto longo|Comentário|
|`CheckBox`|Selecionar opções independentes|Aceitar termos|
|`RadioButton`|Escolher uma opção|Sexo|
|`Switch`|Ligar/desligar|Notificações|
|`Slider`|Selecionar valor em intervalo|Volume|
|`Picker`|Escolher item de uma lista|Cidade|
|`DatePicker`|Escolher data|Nascimento|
|`TimePicker`|Escolher horário|Agendamento|

## 🎯 Forma rápida de memorizar

```
LABEL       → mostra texto
BUTTON      → executa ação
IMAGE       → mostra imagem

ENTRY       → digita uma linha
EDITOR      → digita várias linhas

CHECKBOX    → marca opções
RADIOBUTTON → escolhe uma opção
SWITCH      → liga/desliga

SLIDER      → escolhe um valor
PICKER      → escolhe da lista
DATEPICKER  → escolhe uma data
TIMEPICKER  → escolhe um horário
```

Uma distinção **muito importante para provas e para desenvolvimento MAUI** é:

> **`Entry` ≠ `Editor`** → uma linha vs. várias linhas  
> **`CheckBox` ≠ `RadioButton`** → opções independentes vs. escolha única  
> **`Picker` ≠ `RadioButton`** → lista selecionável vs. opções visíveis na tela  
> **`DatePicker` ≠ `TimePicker`** → data vs. horário