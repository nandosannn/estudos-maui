
O ciclo de vida e a inicialização de um projeto **.NET MAUI** seguem uma cadeia bem definida: a execução parte do código nativo de cada sistema operacional (Android, iOS, macOS, Windows) até convergir para o código compartilhado em C# e XAML.

### Resumo do Fluxo de Execução

| **Ordem** | **Componente / Arquivo**                      | **Plataforma / Camada**       | **Função Principal**                                                                         |
| --------- | --------------------------------------------- | ----------------------------- | -------------------------------------------------------------------------------------------- |
| **1**     | `Platforms/{OS}/*` (ex: `MainApplication.cs`) | Nativa (Android / iOS / etc.) | Ponto de entrada nativo do OS; herda classes base da Microsoft e chama o .NET MAUI.          |
| **2**     | `MauiProgram.cs`                              | Compartilhada (C#)            | Configura o builder, serviços de injeção de dependência (DI), fontes e bibliotecas.          |
| **3**     | `App.xaml` / `App.xaml.cs`                    | Compartilhada (XAML + C#)     | Define recursos globais (cores, estilos) e define a primeira página em `MainPage`.           |
| **4**     | `AppShell.xaml` / `AppShell.xaml.cs`          | Compartilhada (XAML + C#)     | Estrutura a navegação principal (abas, menus flyout) e aponta para a rota inicial.           |
| **5**     | `MainPage.xaml` / `MainPage.xaml.cs`          | Compartilhada (XAML + C#)     | Primeira tela visível ao usuário, contendo os elementos de interface e eventos (ex: clique). |

### 1. Camada Nativa (`Platforms/`)

Cada sistema operacional precisa de um ponto de entrada específico para iniciar o processo.

- **Android (`Platforms/Android/MainApplication.cs`):** A classe herda de `MauiApplication` (que deriva de `Android.App.Application`) e implementa o método obrigatório `CreateMauiApp()`.
    
- **iOS (`Platforms/iOS/AppDelegate.cs`):** Herda de `MauiUIApplicationDelegate` e também executa `CreateMauiApp()`.
    


```C#
// Platforms/Android/MainApplication.cs
[Application]
public class MainApplication : MauiApplication
{
    public MainApplication(IntPtr handle, JniHandleOwnership ownership)
        : base(handle, ownership)
    {
    }

    protected override MauiApp CreateMauiApp() => MauiProgram.CreateMauiApp();
}
```

### 2. Configuração Central (`MauiProgram.cs`)

O `MauiProgram` atua de forma similar ao `Program.cs` do ASP.NET Core: utiliza o padrão **Host Builder** para configurar a aplicação antes que a interface seja montada.



```C#
// MauiProgram.cs
public static class MauiProgram
{
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder();
        builder
            .UseMauiApp<App>() // Aponta para a classe App
            .ConfigureFonts(fonts =>
            {
                fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
                fonts.AddFont("OpenSans-Semibold.ttf", "OpenSansSemibold");
            });

        // Registro de Injeção de Dependências e Serviços (Ex: EF Core, Repositories)
        // builder.Services.AddSingleton<MeuServico>();

        return builder.Build();
    }
}
```

### 3. Aplicação e Recursos Globais (`App.xaml` e `App.xaml.cs`)

Nesta etapa, o conceito de **Code-Behind** é aplicado: o arquivo `.xaml` cuida da declaração de estilos visuais e o `.xaml.cs` cuida da lógica do ciclo de vida da aplicação.

- **`InitializeComponent()`**: Método gerado automaticamente que analisa o arquivo XAML e instancia os objetos correspondentes em tempo de execução.
    
- **`MainPage`**: Propriedade que define qual será a raiz visual da aplicação (geralmente uma instância de `AppShell`).
    


```XML
<!-- App.xaml -->
<Application xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:MeuApp"
             x:Class="MeuApp.App">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="Resources/Styles/Colors.xaml" />
                <ResourceDictionary Source="Resources/Styles/Styles.xaml" />
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```



```C#
// App.xaml.cs
namespace MeuApp;

public partial class App : Application
{
    public App()
    {
        InitializeComponent(); // Lê o XAML e instancia os recursos

        MainPage = new AppShell(); // Define o Shell como estrutura inicial
    }
}
```

### 4. Navegação e Casca do App (`AppShell.xaml`)

O **Shell** organiza a hierarquia de navegação do app (menus laterais, abas inferiores/superiores) e define qual página deve ser renderizada dentro da área de conteúdo inicial.



```XML
<!-- AppShell.xaml -->
<Shell xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
       xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
       xmlns:local="clr-namespace:MeuApp"
       x:Class="MeuApp.AppShell">

    <ShellContent
        Title="Início"
        ContentTemplate="{DataTemplate local:MainPage}"
        Route="MainPage" />
</Shell>
```

### 5. Página Principal e Lógica de Interface (`MainPage`)

A tela final reúne os elementos visuais declarados no XAML e os eventos manipulados no Code-Behind C#.



```XML
<!-- MainPage.xaml -->
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="MeuApp.MainPage">

    <ScrollView>
        <VerticalStackLayout Spacing="25" Padding="30">
            <Label Text="Bem-vindo ao .NET MAUI!" FontSize="20" HorizontalOptions="Center" />
            <Button x:Name="CounterBtn"
                    Text="Clique aqui"
                    Clicked="OnCounterClicked"
                    HorizontalOptions="Center" />
        </VerticalStackLayout>
    </ScrollView>
</ContentPage>
```



```C#
// MainPage.xaml.cs
namespace MeuApp;

public partial class MainPage : ContentPage
{
    private int count = 0;

    public MainPage()
    {
        InitializeComponent();
    }

    private void OnCounterClicked(object sender, EventArgs e)
    {
        count++;

        if (count == 1)
            CounterBtn.Text = $"Clicado {count} vez";
        else
            CounterBtn.Text = $"Clicado {count} vezes";

        SemanticScreenReader.Announce(CounterBtn.Text);
    }
}
```

### Diferença Fundamental: XAML vs Code-Behind

|**Característica**|**XAML (.xaml)**|**Code-Behind (.xaml.cs)**|
|---|---|---|
|**Papel**|Camada visual declarativa (UI).|Lógica procedural e eventos.|
|**Execução**|Convertido em objetos C# via `InitializeComponent()`.|Compilado diretamente pelo compilador C# Roslyn.|
|**Elementos comuns**|`Button`, `Label`, `ResourceDictionary`, Estilos.|Métodos manipuladores de eventos (`OnClick`), variáveis de estado, chamadas de serviço.|
