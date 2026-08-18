
A aula demonstra o processo inicial de criação de uma solução multi-projetos no Visual Studio utilizando o **.NET MAUI**, destacando a evolução da arquitetura em relação ao seu antecessor direto, o **Xamarin.Forms**.

### Passo a Passo: Criação e Organização do Projeto

1. **Seleção de Template:**
    
    - No Visual Studio, busca-se por **MAUI**.
        
    - Escolhe-se o template **.NET MAUI App** (Aplicativo .NET MAUI).
        
2. **Configuração de Nomes e Pastas:**
    
    - **Nome da Solução:** `ProjetosMaui` (centralizará os múltiplos apps do curso).
        
    - **Nome do Projeto:** `AppNumeroDaSorte` (primeiro aplicativo prático).
        
    - **Organização em Pastas de Solução (_Solution Folders_):** Criação da pasta lógica `EP01` para encapsular o projeto do capítulo.
        
3. **Versão do Target Framework:**
    
    - Criação focada no **.NET 6** (LTS à época da gravação), com menção à compatibilidade com o **.NET 7+**.
        

### Comparativo Arquitetural: .NET MAUI vs. Xamarin.Forms

|**Característica**|**Xamarin.Forms (Legado)**|**.NET MAUI (Atual)**|
|---|---|---|
|**Estrutura de Projetos**|Múltiplos projetos (`.Android`, `.iOS`, `.UWP`, `.Core`).|**Single Project** (um único projeto C# multiplataforma).|
|**Seleção de Plataforma**|Trocar o _Startup Project_ na solução.|Dropdown único no seletor de execução do Visual Studio.|
|**Gerenciamento de Assets**|Imagens e fontes duplicadas por pasta nativa em várias resoluções.|Pasta unificada `Resources/` com redimensionamento automático.|
|**Código Nativo**|Isolado em projetos separados via `DependencyService` / _Custom Renderers_.|Centralizado na pasta interna `Platforms/` via _Handlers_.|

### Estrutura de Pastas e Arquivos do .NET MAUI

#### 1. `Dependencies/`

Gerencia referências e bibliotecas divididas por plataforma de destino:

- SDKs base do .NET.
    
- Pacotes NuGet específicos do MAUI.
    
- APIs e bibliotecas de bindings de cada SO (Android SDK, iOS bindings, Windows App SDK).
    

#### 2. `Platforms/`

Armazena os pontos de entrada de ciclo de vida e manifestos de cada sistema operacional:

Plaintext

```
Platforms/
├── Android/         -> MainActivity.cs, MainApplication.cs, AndroidManifest.xml
├── iOS/             -> AppDelegate.cs, Program.cs, Info.plist
├── MacCatalyst/     -> AppDelegate.cs, Program.cs, Info.plist
├── Tizen/           -> Main.cs, tizen-manifest.xml
└── Windows/         -> App.xaml, App.xaml.cs, Package.appxmanifest
```

#### 3. `Resources/`

Centraliza todos os ativos visuais. O compilador do MAUI processa e gera os arquivos nos formatos e densidades corretos para cada plataforma:

|**Subpasta**|**Função**|
|---|---|
|`AppIcon/`|Ícone do aplicativo (gera automaticamente para todas as densidades).|
|`Fonts/`|Fontes `.ttf` ou `.otf` compartilhadas.|
|`Images/`|Imagens e vetores `.svg` redimensionados em tempo de compilação.|
|`Raw/`|Arquivos estáticos brutos (JSONs, dados locais).|
|`Splash/`|Tela de inicialização (_Splash Screen_).|
|`Styles/`|Dicionários de recursos XAML com cores e temas (`Styles.xaml`, `Colors.xaml`).|

### Template Padrão e Exemplo de Código

O template base criado gera uma tela com um contador de cliques demonstrando a ligação entre o XAML (_View_) e o C# (_Code-Behind_):

**Exemplo do Layout (`MainPage.xaml`):**

XML

```C#
<ScrollView>
    <VerticalStackLayout Spacing="25" Padding="30">
        <!-- Robô mascote do .NET -->
        <Image Source="dotnet_bot.svg" HeightRequest="185" />

        <Label Text="Hello, World!" FontSize="32" HorizontalOptions="Center" />
        <Label Text="Welcome to .NET MAUI" FontSize="18" HorizontalOptions="Center" />

        <!-- Botão interativo -->
        <Button x:Name="CounterBtn"
                Text="Click me"
                Clicked="OnCounterClicked"
                HorizontalOptions="Center" />
    </VerticalStackLayout>
</ScrollView>
```

**Exemplo da Lógica (`MainPage.xaml.cs`):**

C#

```C#
public partial class MainPage : ContentPage
{
    int count = 0;

    public MainPage()
    {
        InitializeComponent();
    }

    private void OnCounterClicked(object sender, EventArgs e)
    {
        count++;

        if (count == 1)
            CounterBtn.Text = $"Clicked {count} time";
        else
            CounterBtn.Text = $"Clicked {count} times";

        SemanticScreenReader.Announce(CounterBtn.Text);
    }
}
```