# .NET MAUI — Construção do Projeto MAUI Gallery

## 1. Objetivo do projeto

O **MAUI Gallery** será um aplicativo utilizado para apresentar diversos componentes disponíveis por padrão no **.NET MAUI**.

A ideia é criar uma espécie de **galeria de componentes**, onde:

- A tela inicial lista os componentes disponíveis.
    
- O usuário seleciona um componente.
    
- Uma nova página demonstra como aquele componente funciona.
    
- São apresentadas suas principais propriedades e possibilidades de configuração.
    
- O aplicativo também utiliza um **FlyoutPage** para organizar os componentes em um menu lateral.
    

### Estrutura conceitual

```text
MAUI Gallery
│
├── Menu lateral (Flyout)
│   ├── Componentes
│   ├── Layouts
│   ├── Controles
│   └── Outros recursos
│
└── Tela principal
    └── Lista de componentes
        └── Página de demonstração
```

---

# 2. Preparação dos recursos visuais

Antes de iniciar o desenvolvimento, foram preparados os arquivos gráficos do aplicativo.

Entre os recursos utilizados estão:

|Recurso|Finalidade|
|---|---|
|Ícone principal|Identificação do aplicativo|
|Ícone para Android|Versão adaptada para Android|
|Imagem de fundo|Composição visual do ícone|
|Splash Screen|Tela exibida durante a inicialização|
|Logo|Identificação visual do MAUI Gallery|

Os arquivos foram organizados dentro do projeto para facilitar a manutenção.

---

# 3. Criação do projeto

Foi criado um novo projeto utilizando **.NET MAUI**.

O projeto foi denominado:

```text
MAUI Gallery
```

A ideia é utilizar esse projeto especificamente para a demonstração dos componentes do MAUI.

---

# 4. Organização dos arquivos

Foi criada uma pasta específica para a Splash Screen:

```text
Resources/
│
├── AppIcon/
│   ├── ícones
│   └── ícone Android
│
└── Splash/
    └── splash screen
```

Os ícones existentes no projeto foram substituídos pelos arquivos preparados anteriormente.

### Boa prática apresentada

A aula recomenda **substituir os arquivos padrão do projeto**, em vez de criar vários arquivos com nomes diferentes.

Isso ajuda a evitar problemas relacionados à configuração e ao funcionamento dos recursos do MAUI em determinadas plataformas.

---

# 5. Configuração pelo arquivo `.csproj`

Algumas configurações do aplicativo são realizadas diretamente no arquivo de projeto:

```text
Projeto.csproj
```

Esse arquivo permite configurar informações como:

- Nome do aplicativo;
    
- Namespace;
    
- Versão;
    
- Ícone;
    
- Splash Screen;
    
- Recursos específicos de cada plataforma.
    

---

# 6. Nome, namespace e versão

Foram configuradas informações básicas do aplicativo, como o nome e a versão.

Exemplo conceitual:

```xml
<ApplicationTitle>MAUI Gallery</ApplicationTitle>

<RootNamespace>...</RootNamespace>

<ApplicationDisplayVersion>1.0</ApplicationDisplayVersion>

<ApplicationVersion>1</ApplicationVersion>
```

### Diferença entre as versões

|Configuração|Finalidade|
|---|---|
|`ApplicationDisplayVersion`|Versão exibida para o usuário, por exemplo `1.0.0`|
|`ApplicationVersion`|Número sequencial utilizado para identificar versões do aplicativo|

Exemplo:

```text
ApplicationDisplayVersion = 1.0.0
ApplicationVersion = 1
```

---

# 7. Configuração do ícone

O ícone do aplicativo é composto por diferentes elementos.

A configuração utiliza uma imagem de fundo e uma imagem em primeiro plano:

```xml
<MauiIcon
    Include="Resources\AppIcon\..."
    ForegroundFile="Resources\AppIcon\..."
    Color="#F9F9F9" />
```

### Elementos importantes

|Propriedade|Função|
|---|---|
|`MauiIcon`|Define o ícone do aplicativo|
|`Include`|Define o arquivo principal do ícone|
|`ForegroundFile`|Define a imagem em primeiro plano|
|`Color`|Define a cor de fundo|

A cor utilizada na configuração apresentada na aula foi:

```text
#F9F9F9
```

---

# 8. Configuração da Splash Screen

A **Splash Screen** é a tela apresentada enquanto o aplicativo está sendo inicializado.

Exemplo:

```xml
<MauiSplashScreen
    Include="Resources\Splash\splash.svg"
    Color="#F9F9F9"
    BaseSize="154,188" />
```

### Principais propriedades

|Propriedade|Função|
|---|---|
|`MauiSplashScreen`|Define a Splash Screen|
|`Include`|Indica o arquivo utilizado|
|`Color`|Define a cor de fundo|
|`BaseSize`|Define o tamanho base da imagem|

No exemplo apresentado:

```text
Cor: #F9F9F9
BaseSize: 154 x 188
```

---

# 9. Configuração específica para Android

O Android possui algumas particularidades no tratamento dos ícones.

Por isso, foi criada uma configuração específica utilizando uma condição do **MSBuild**:

```xml
Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'android'"
```

A ideia é utilizar um ícone diferente quando o aplicativo for compilado para Android.

Conceitualmente:

```xml
<MauiIcon
    Include="Resources\AppIcon\icon.svg"
    ForegroundFile="Resources\AppIcon\icon_android.svg"
    Color="#F9F9F9"
    Condition="...android..." />
```

---

# 10. Por que utilizar um ícone diferente no Android?

O Android possui regras próprias para composição e dimensionamento dos ícones.

Na aula, foi utilizada uma versão do ícone aproximadamente **40% menor** para adequá-lo melhor ao sistema.

Assim:

```text
Outras plataformas
    ↓
Ícone padrão

Android
    ↓
Ícone adaptado
```

Isso permite obter uma aparência mais adequada em diferentes sistemas operacionais.

---

# 11. `Condition` no `.csproj`

O atributo `Condition` permite que uma determinada configuração seja aplicada somente quando uma condição específica for verdadeira.

Exemplo conceitual:

```xml
Condition="plataforma == Android"
```

Nesse caso:

```text
Se plataforma = Android
        ↓
Utiliza configuração específica

Caso contrário
        ↓
Utiliza configuração padrão
```

Esse recurso é importante em aplicações .NET MAUI porque o mesmo projeto pode ser executado em diferentes plataformas.

---

# 12. Estrutura do MAUI Gallery

O projeto será desenvolvido para demonstrar diversos componentes:

```text
MAUI Gallery
│
├── Flyout
│   └── Menu lateral
│
├── Página inicial
│   └── Lista de componentes
│
├── Componentes
│   ├── Button
│   ├── Label
│   ├── Entry
│   ├── Image
│   ├── Slider
│   ├── Switch
│   └── ...
│
└── Página de demonstração
    └── Propriedades e funcionamento
```

---

# 13. Resumo dos principais conceitos

|Conceito|Resumo|
|---|---|
|**MAUI Gallery**|Aplicativo criado para demonstrar componentes do .NET MAUI|
|**Flyout**|Menu lateral utilizado para navegar entre os componentes|
|**`.csproj`**|Arquivo de configuração do projeto|
|**`MauiIcon`**|Configuração do ícone do aplicativo|
|**`MauiSplashScreen`**|Configuração da Splash Screen|
|**`ForegroundFile`**|Define a imagem em primeiro plano do ícone|
|**`Color`**|Define a cor de fundo do recurso|
|**`BaseSize`**|Define o tamanho base da imagem|
|**`Condition`**|Permite aplicar configurações específicas para determinada plataforma|
|**`ApplicationTitle`**|Define o nome do aplicativo|
|**`ApplicationDisplayVersion`**|Define a versão apresentada ao usuário|
|**`ApplicationVersion`**|Define o número de versão utilizado internamente|
|**Ícone específico para Android**|Permite adaptar o ícone às características do Android|

---

## 14. Ideia principal da aula

A primeira etapa da construção do **MAUI Gallery** não envolve ainda a criação dos componentes da galeria. O foco foi preparar a estrutura inicial do projeto e seus recursos visuais.

O fluxo apresentado foi:

```text
Preparar imagens
       ↓
Criar projeto MAUI
       ↓
Organizar ícones e Splash Screen
       ↓
Substituir recursos padrão
       ↓
Configurar o arquivo .csproj
       ↓
Configurar nome e versão
       ↓
Configurar ícone
       ↓
Configurar Splash Screen
       ↓
Criar configuração específica para Android
       ↓
Próxima etapa:
desenvolvimento da galeria
```

**Conclusão:** nesta aula foram preparadas as bases do projeto **MAUI Gallery**, principalmente a identidade visual e as configurações específicas do projeto. Na próxima etapa, o desenvolvimento passa para a construção da interface e da galeria de componentes.