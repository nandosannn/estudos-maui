# 📱 Roadmap básico de .NET MAUI

### 1. Fundamentos do .NET MAUI

- [x]  O que é .NET MAUI
- [x]  Diferença entre .NET MAUI, Xamarin.Forms e desenvolvimento nativo
- [x]  Multiplataforma: Android, iOS, Windows e MacCatalyst
- [x]  Estrutura de um projeto MAUI
- [x]  `MauiProgram.cs`
- [x]  `App.xaml` e `App.xaml.cs`
- [x]  `AppShell.xaml`
- [x]  `MainPage.xaml`
- [x]  Code-behind (`.xaml.cs`)
- [x]  Ciclo de vida básico da aplicação

---

### 2. XAML

- [x]  O que é XAML
- [x]  Sintaxe do XAML
- [x]  Elementos e atributos
- [x]  `x:Name`
- [x]  Namespaces
- [x]  Eventos
- [x]  Propriedades
- [x]  `StaticResource`
- [x]  `DynamicResource`
- [x]  Styles
- [x]  Resources

**Componentes básicos:**

- [x]  `Label`
- [x]  `Button`
- [x]  `Image`
- [x]  `Entry`
- [x]  `Editor`
- [x]  `CheckBox`
- [x]  `RadioButton`
- [x]  `Switch`
- [x]  `Slider`
- [x]  `Picker`
- [x]  `DatePicker`
- [x]  `TimePicker`

---

### 3. Layouts

Entender como organizar os elementos na tela:

- [x]  `VerticalStackLayout`
- [x]  `HorizontalStackLayout`
- [x]  `Grid`
- [x]  `FlexLayout`
- [x]  `ScrollView`
- [x]  `AbsoluteLayout`

E principalmente:

- [x]  `Padding`
- [x]  `Margin`
- [x]  `Spacing`
- [x]  `WidthRequest`
- [x]  `HeightRequest`
- [x]  `HorizontalOptions`
- [x]  `VerticalOptions`
- [x]  `RowDefinitions`
- [x]  `ColumnDefinitions`

---

### 4. Navegação

- [x]  `Shell`
- [x]  Rotas
- [x]  Navegação entre páginas
- [x]  `GoToAsync()`
- [x]  Passagem de parâmetros
- [x]  Navegação para trás
- [x]  `NavigationPage`
- [x]  `FlyoutPage`
- [x]  `TabbedPage`
- [x]  Deep links

---

### 5. Controles e interfaces

Depois dos componentes básicos:

- [ ]  `CollectionView`
- [ ]  `ListView`
- [ ]  `CarouselView`
- [ ]  `Border`
- [ ]  `Frame`
- [ ]  `SwipeView`
- [ ]  `RefreshView`
- [ ]  `ActivityIndicator`
- [ ]  `ProgressBar`
- [ ]  `WebView`

---

### 6. Eventos e interação

- [ ]  Eventos no XAML
- [ ]  Event handlers
- [ ]  `Clicked`
- [ ]  `TextChanged`
- [ ]  `CheckedChanged`
- [ ]  `SelectionChanged`
- [ ]  Gestos
- [ ]  `TapGestureRecognizer`
- [ ]  `SwipeGestureRecognizer`

---

# 🧠 7. Data Binding — MUITO importante

Esse é um dos assuntos que você deve dominar.

- [ ]  O que é Data Binding
- [ ]  Binding de propriedades
- [ ]  `BindingContext`
- [ ]  `OneWay`
- [ ]  `TwoWay`
- [ ]  `OneTime`
- [ ]  `OneWayToSource`
- [ ]  Binding entre controles
- [ ]  Binding de objetos
- [ ]  Binding de listas
- [ ]  `INotifyPropertyChanged`
- [ ]  `ObservableCollection`
- [ ]  `Command`
- [ ]  `ICommand`

Exemplo:

```
<Entry Text="{Binding Nome}" />

<Label Text="{Binding Nome}" />
```

---

# 🏗️ 8. MVVM

Depois de entender Binding:

- [ ]  O que é MVVM
- [ ]  Model
- [ ]  View
- [ ]  ViewModel
- [ ]  Separação de responsabilidades
- [ ]  `INotifyPropertyChanged`
- [ ]  `ICommand`
- [ ]  CommunityToolkit.Mvvm
- [ ]  `ObservableObject`
- [ ]  `ObservableProperty`
- [ ]  `RelayCommand`
- [ ]  Injeção de dependência no ViewModel

Esse é um dos pontos **mais importantes para desenvolvimento profissional em MAUI**.

---

# 🌐 9. Consumo de APIs

Como você já está trabalhando com APIs, essa parte será especialmente importante.

- [ ]  `HttpClient`
- [ ]  GET
- [ ]  POST
- [ ]  PUT
- [ ]  DELETE
- [ ]  JSON
- [ ]  Serialização
- [ ]  Desserialização
- [ ]  DTOs
- [ ]  Tratamento de erros HTTP
- [ ]  Headers
- [ ]  Bearer Token
- [ ]  Autenticação
- [ ]  Interceptação de requisições
- [ ]  `HttpClientFactory`
- [ ]  APIs REST

Exemplo de fluxo:

```
MAUI
  ↓
HttpClient
  ↓
API REST
  ↓
Laravel / Spring Boot / ASP.NET
  ↓
Banco de dados
```

---

# 🔐 10. Armazenamento de dados

- [ ]  `Preferences`
- [ ]  `SecureStorage`
- [ ]  SQLite
- [ ]  Entity Framework Core
- [ ]  Banco local
- [ ]  Cache
- [ ]  Persistência offline
- [ ]  Sincronização com API

Especialmente:

```
await SecureStorage.SetAsync("auth_token", token);
```

e

```
var token = await SecureStorage.GetAsync("auth_token");
```

---

# 🔑 11. Autenticação

- [ ]  Login
- [ ]  Logout
- [ ]  Cadastro
- [ ]  Token JWT
- [ ]  Bearer Token
- [ ]  SecureStorage
- [ ]  Controle de sessão
- [ ]  Expiração de token
- [ ]  Refresh Token
- [ ]  Redirecionamento após login
- [ ]  Rotas protegidas

---

# 💉 12. Dependency Injection

Muito importante no .NET.

- [ ]  O que é DI
- [ ]  `AddSingleton`
- [ ]  `AddTransient`
- [ ]  `AddScoped`
- [ ]  Registro de serviços
- [ ]  Injeção via construtor
- [ ]  Service Layer
- [ ]  Repository Pattern

Exemplo:

```
builder.Services.AddSingleton<ApiService>();
```

Depois:

```
public MainPage(ApiService apiService)
{
    InitializeComponent();
}
```

---

# 🎨 13. Estilização

- [ ]  `Style`
- [ ]  `ResourceDictionary`
- [ ]  Cores
- [ ]  Fontes
- [ ]  Tamanhos
- [ ]  Temas
- [ ]  Dark Mode
- [ ]  Estilos globais
- [ ]  `App.xaml`
- [ ]  `VisualStateManager`

---

# 📱 14. Recursos específicos de dispositivo

Uma das grandes vantagens do MAUI.

- [ ]  Camera
- [ ]  GPS/Geolocalização
- [ ]  Microfone
- [ ]  Galeria
- [ ]  Arquivos
- [ ]  Notificações
- [ ]  Vibração
- [ ]  Conectividade
- [ ]  Bateria
- [ ]  Device information
- [ ]  Launcher
- [ ]  Browser
- [ ]  Share

---

# ⚙️ 15. Plataformas

Entender que MAUI é multiplataforma, mas cada plataforma possui particularidades.

- [ ]  Android
- [ ]  Windows
- [ ]  iOS
- [ ]  MacCatalyst
- [ ]  `Platforms/Android`
- [ ]  `Platforms/Windows`
- [ ]  `Platforms/iOS`
- [ ]  Código específico de plataforma
- [ ]  `#if ANDROID`
- [ ]  Handlers
- [ ]  Configurações específicas de cada plataforma

---

# 🔧 16. Handlers

Um assunto mais intermediário:

- [ ]  O que são Handlers
- [ ]  Como MAUI transforma controles em componentes nativos
- [ ]  Customização de controles
- [ ]  `Mapper`
- [ ]  Handlers específicos por plataforma

Isso ajuda bastante a entender **por que um componente pode aparecer diferente no Android e no Windows**.

---

# 🧩 17. .NET MAUI Community Toolkit

- [ ]  Instalação
- [ ]  Behaviors
- [ ]  Converters
- [ ]  Popups
- [ ]  Animations
- [ ]  Effects
- [ ]  `EventToCommandBehavior`
- [ ]  `MediaElement`
- [ ]  `TouchEffect`

---

# 🧪 18. Debug e testes

- [ ]  Debug no Visual Studio
- [ ]  Breakpoints
- [ ]  Watch
- [ ]  Output
- [ ]  Logs
- [ ]  Exceptions
- [ ]  Debug Android
- [ ]  Android Emulator
- [ ]  Hot Reload
- [ ]  Unit Tests
- [ ]  Testes de ViewModel

---

# 📦 19. Build e publicação

- [ ]  Build
- [ ]  Release
- [ ]  Debug vs Release
- [ ]  APK
- [ ]  AAB
- [ ]  Assinatura do aplicativo
- [ ]  Keystore
- [ ]  Versionamento
- [ ]  Google Play
- [ ]  Microsoft Store
- [ ]  CI/CD

---

# 🏛️ 20. Arquitetura de aplicações

Depois de dominar os anteriores:

- [ ]  MVVM
- [ ]  Clean Architecture
- [ ]  Repository Pattern
- [ ]  Service Layer
- [ ]  DTO
- [ ]  Dependency Injection
- [ ]  SOLID
- [ ]  Separação de responsabilidades
- [ ]  Tratamento global de erros
- [ ]  Logging
- [ ]  Cache
- [ ]  Offline First

---

## 🎯 Ordem que eu recomendo para você

Como você **já está fazendo um curso de MAUI e já passou por páginas, layouts, Flyout/Tabbed e começou a seção 5**, eu seguiria esta sequência:

| Ordem | Assunto                   | Prioridade |
| ----- | ------------------------- | ---------- |
| 1     | Fundamentos do MAUI       | ⭐⭐⭐        |
| 2     | XAML                      | ⭐⭐⭐        |
| 3     | Layouts                   | ⭐⭐⭐        |
| 4     | Controles                 | ⭐⭐⭐        |
| 5     | Navegação/Shell           | ⭐⭐⭐        |
| 6     | Eventos                   | ⭐⭐         |
| 7     | **Data Binding**          | ⭐⭐⭐⭐⭐      |
| 8     | **MVVM**                  | ⭐⭐⭐⭐⭐      |
| 9     | **Dependency Injection**  | ⭐⭐⭐⭐⭐      |
| 10    | **Consumo de APIs**       | ⭐⭐⭐⭐⭐      |
| 11    | JSON/DTO                  | ⭐⭐⭐⭐       |
| 12    | Autenticação/JWT          | ⭐⭐⭐⭐⭐      |
| 13    | SecureStorage/Preferences | ⭐⭐⭐⭐       |
| 14    | SQLite                    | ⭐⭐⭐⭐       |
| 15    | CommunityToolkit          | ⭐⭐⭐        |
| 16    | Recursos do dispositivo   | ⭐⭐⭐        |
| 17    | Handlers                  | ⭐⭐⭐        |
| 18    | Testes/Debug              | ⭐⭐⭐        |
| 19    | Build/Publicação          | ⭐⭐⭐        |
| 20    | Clean Architecture        | ⭐⭐⭐⭐       |