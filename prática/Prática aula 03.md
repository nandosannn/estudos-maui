## 📱 Mini projeto: Formulário de Preferências

### 🎯 Componentes utilizados

- `Label`
- `Button`
- `Image`
- `Entry`
- `Editor`
- `CheckBox`
- `RadioButton`
- `Switch`
- `Slider`
- `Picker`
- `DatePicker`
- `TimePicker`

---

# 1. Crie o projeto

No Visual Studio:

```
Criar novo projeto
        ↓
.NET MAUI App
        ↓
Nome: FormularioPreferencias
```

Vamos trabalhar principalmente com:

```
MainPage.xaml
MainPage.xaml.cs
```

---

# 2. Interface — `MainPage.xaml`

Substitua o conteúdo pelo código abaixo:

```xml
<?xml version="1.0" encoding="utf-8" ?>

<ContentPage
    xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
    x:Class="FormularioPreferencias.MainPage"
    Title="Meu Perfil">

    <ScrollView>

        <VerticalStackLayout
            Padding="20"
            Spacing="15">

            <!-- TÍTULO -->
            <Label
                Text="Meu Perfil"
                FontSize="30"
                FontAttributes="Bold"
                HorizontalOptions="Center" />

            <!-- IMAGE -->
            <Image
                Source="dotnet_bot.png"
                HeightRequest="120"
                Aspect="AspectFit" />

            <!-- ENTRY -->
            <Label
                Text="Nome:" />

            <Entry
                x:Name="NomeEntry"
                Placeholder="Digite seu nome"
                MaxLength="50" />

            <!-- PICKER -->
            <Label
                Text="Cidade:" />

            <Picker
                x:Name="CidadePicker"
                Title="Selecione sua cidade">

                <Picker.Items>
                    <x:String>Natal</x:String>
                    <x:String>Recife</x:String>
                    <x:String>João Pessoa</x:String>
                    <x:String>Fortaleza</x:String>
                </Picker.Items>

            </Picker>

            <!-- DATEPICKER -->
            <Label
                Text="Data de nascimento:" />

            <DatePicker
                x:Name="DataNascimentoPicker"
                MaximumDate="2026-08-31" />

            <!-- TIMEPICKER -->
            <Label
                Text="Horário preferido para estudar:" />

            <TimePicker
                x:Name="HorarioPicker"
                Time="08:00:00" />

            <!-- RADIOBUTTON -->
            <Label
                Text="Turno preferido:" />

            <RadioButton
                x:Name="ManhaRadio"
                Content="Manhã"
                GroupName="Turno"
                Value="Manhã" />

            <RadioButton
                x:Name="TardeRadio"
                Content="Tarde"
                GroupName="Turno"
                Value="Tarde" />

            <RadioButton
                x:Name="NoiteRadio"
                Content="Noite"
                GroupName="Turno"
                Value="Noite" />

            <!-- CHECKBOX -->
            <HorizontalStackLayout>

                <CheckBox
                    x:Name="TecnologiaCheckBox" />

                <Label
                    Text="Gosto de tecnologia"
                    VerticalOptions="Center" />

            </HorizontalStackLayout>

            <HorizontalStackLayout>

                <CheckBox
                    x:Name="JogosCheckBox" />

                <Label
                    Text="Gosto de jogos"
                    VerticalOptions="Center" />

            </HorizontalStackLayout>

            <HorizontalStackLayout>

                <CheckBox
                    x:Name="FilmesCheckBox" />

                <Label
                    Text="Gosto de filmes"
                    VerticalOptions="Center" />

            </HorizontalStackLayout>

            <!-- SWITCH -->
            <HorizontalStackLayout>

                <Label
                    Text="Receber notificações"
                    VerticalOptions="Center" />

                <Switch
                    x:Name="NotificacoesSwitch"
                    IsToggled="True" />

            </HorizontalStackLayout>

            <!-- SLIDER -->
            <Label
                Text="Quantas horas você estuda por dia?" />

            <Slider
                x:Name="HorasSlider"
                Minimum="0"
                Maximum="12"
                Value="4"
                ValueChanged="OnSliderValueChanged" />

            <Label
                x:Name="HorasLabel"
                Text="4 horas"
                HorizontalOptions="Center"
                FontSize="20"
                FontAttributes="Bold" />

            <!-- EDITOR -->
            <Label
                Text="Conte um pouco sobre você:" />

            <Editor
                x:Name="DescricaoEditor"
                Placeholder="Digite uma descrição..."
                HeightRequest="120"
                AutoSize="TextChanges" />

            <!-- BUTTON -->
            <Button
                Text="Enviar formulário"
                Clicked="OnEnviarClicked" />

            <!-- RESULTADO -->
            <Label
                x:Name="ResultadoLabel"
                FontSize="16"
                LineBreakMode="WordWrap"
                IsVisible="False" />

        </VerticalStackLayout>

    </ScrollView>

</ContentPage>
```

---

# 3. Lógica — `MainPage.xaml.cs`

Agora abra:

```
MainPage.xaml.cs
```

E coloque:

```C#
namespace FormularioPreferencias;

public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
    }

    private void OnSliderValueChanged(
        object sender,
        ValueChangedEventArgs e)
    {
        HorasLabel.Text = $"{Math.Round(e.NewValue)} horas";
    }

    private async void OnEnviarClicked(
        object sender,
        EventArgs e)
    {
        string nome = NomeEntry.Text;

        string cidade = CidadePicker.SelectedItem?.ToString();

        DateTime dataNascimento =
            DataNascimentoPicker.Date;

        TimeSpan horario =
            HorarioPicker.Time;

        string turno = "";

        if (ManhaRadio.IsChecked)
        {
            turno = "Manhã";
        }
        else if (TardeRadio.IsChecked)
        {
            turno = "Tarde";
        }
        else if (NoiteRadio.IsChecked)
        {
            turno = "Noite";
        }

        List<string> interesses = new();

        if (TecnologiaCheckBox.IsChecked)
        {
            interesses.Add("Tecnologia");
        }

        if (JogosCheckBox.IsChecked)
        {
            interesses.Add("Jogos");
        }

        if (FilmesCheckBox.IsChecked)
        {
            interesses.Add("Filmes");
        }

        bool receberNotificacoes =
            NotificacoesSwitch.IsToggled;

        double horasEstudo =
            Math.Round(HorasSlider.Value);

        string descricao =
            DescricaoEditor.Text;

        string interessesTexto =
            interesses.Count > 0
                ? string.Join(", ", interesses)
                : "Nenhum";

        string resultado =
            $"Nome: {nome}\n\n" +
            $"Cidade: {cidade}\n\n" +
            $"Data de nascimento: " +
            $"{dataNascimento:dd/MM/yyyy}\n\n" +
            $"Horário de estudo: {horario}\n\n" +
            $"Turno: {turno}\n\n" +
            $"Interesses: {interessesTexto}\n\n" +
            $"Notificações: " +
            $"{(receberNotificacoes ? "Sim" : "Não")}\n\n" +
            $"Horas de estudo: {horasEstudo}\n\n" +
            $"Descrição: {descricao}";

        ResultadoLabel.Text = resultado;

        ResultadoLabel.IsVisible = true;

        await DisplayAlert(
            "Sucesso",
            "Formulário enviado!",
            "OK");
    }
}
```

---

# 🧠 O que você está praticando

## `x:Name`

O `x:Name` permite acessar o componente no C#.

Exemplo:

```
<Entry
    x:Name="NomeEntry" />
```

Depois:

```
string nome = NomeEntry.Text;
```

Fluxo:

```
XAML
 ↓
<Entry x:Name="NomeEntry" />
 ↓
C#
 ↓
NomeEntry.Text
```

---

## Eventos

Você também está trabalhando com eventos.

### Slider

```
<Slider
    ValueChanged="OnSliderValueChanged" />
```

Quando o valor mudar:

```
private void OnSliderValueChanged(
    object sender,
    ValueChangedEventArgs e)
{
    HorasLabel.Text =
        $"{Math.Round(e.NewValue)} horas";
}
```

---

### Button

```
<Button
    Text="Enviar formulário"
    Clicked="OnEnviarClicked" />
```

Quando o usuário clicar:

```
private async void OnEnviarClicked(
    object sender,
    EventArgs e)
{
    // código executado
}
```

---

# 🔄 Fluxo do aplicativo

```
              ┌──────────────┐
              │    Label     │
              │ Título/texto │
              └──────┬───────┘
                     │
              ┌──────▼───────┐
              │    Image     │
              │    Imagem    │
              └──────┬───────┘
                     │
        ┌────────────▼────────────┐
        │   Entrada de dados      │
        │                         │
        │ Entry                   │
        │ Picker                  │
        │ DatePicker              │
        │ TimePicker              │
        │ Editor                  │
        └────────────┬────────────┘
                     │
        ┌────────────▼────────────┐
        │       Escolhas          │
        │                         │
        │ CheckBox                │
        │ RadioButton             │
        │ Switch                  │
        │ Slider                  │
        └────────────┬────────────┘
                     │
              ┌──────▼───────┐
              │    Button    │
              │    Enviar    │
              └──────┬───────┘
                     │
              ┌──────▼───────┐
              │      C#      │
              │ Processamento│
              └──────┬───────┘
                     │
              ┌──────▼───────┐
              │    Label     │
              │   Resultado  │
              └──────────────┘
```

---

# 📋 Checklist de aprendizado

Depois de terminar, tente modificar o projeto sozinho:

- [ ]  Alterar o tamanho do título.
- [ ]  Alterar a imagem.
- [ ]  Adicionar um campo de e-mail usando `Entry`.
- [ ]  Usar `Keyboard="Email"`.
- [ ]  Adicionar mais opções ao `Picker`.
- [ ]  Adicionar outro grupo de `RadioButton`.
- [ ]  Criar mais interesses com `CheckBox`.
- [ ]  Alterar o intervalo do `Slider`.
- [ ]  Mostrar o valor do `Slider` em tempo real.
- [ ]  Alterar a data mínima e máxima do `DatePicker`.
- [ ]  Definir outro horário inicial no `TimePicker`.
- [ ]  Desabilitar o botão quando o nome estiver vazio.
- [ ]  Melhorar o resultado visualmente usando `Border`.

## 🚀 Desafio final

Quando esse projeto estiver funcionando, faça uma versão **sem copiar o código**, criando um **Formulário de Cadastro de Aluno** com:

```
Nome
E-mail
Senha
Curso
Data de nascimento
Turno
Disciplinas favoritas
Receber notificações
Horas disponíveis para estudar
Observações
Botão Cadastrar
```

Esse desafio vai fazer você praticar praticamente todos os componentes básicos da aula e também a conexão entre **XAML + Code Behind (`.xaml.cs`)**, que é uma das bases que você está estudando agora no .NET MAUI.