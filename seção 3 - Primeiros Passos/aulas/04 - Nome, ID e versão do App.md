
A configuração de identidade, plataformas e versionamento no **.NET MAUI** pode ser feita de duas formas principais: visualmente pela **Janela de Propriedades do Projeto** no Visual Studio ou diretamente editando o arquivo de projeto XML (`.csproj`).

O .NET MAUI centraliza essas definições e as propaga automaticamente para os manifestos nativos (`AndroidManifest.xml`, `Info.plist`, etc.), permitindo também sobrescritas específicas por plataforma se necessário.

### Visão Geral dos Parâmetros de Configuração

|**Parâmetro no VS**|**Tag no .csproj**|**Tipo / Formato**|**Descrição e Uso**|
|---|---|---|---|
|**Título do Aplicativo**|`ApplicationTitle`|Texto (`String`)|Nome exibido na tela inicial do dispositivo (abaixo do ícone).|
|**ID do Aplicativo**|`ApplicationId`|Domínio Reverso (`com.empresa.app`)|Identificador único global usado pelas lojas (Play Store / App Store).|
|**ID do Aplicativo (GUID)**|`ApplicationIdGuid`|Formato GUID (`UUID`)|Identificador único exclusivo em formato hexadecimal gerado automaticamente.|
|**Versão de Exibição**|`ApplicationDisplayVersion`|Texto / SemVer (ex: `1.0.0`)|Versão visível ao usuário final na loja e nas telas de "Sobre".|
|**Versão do Aplicativo**|`ApplicationVersion`|Inteiro (`Integer`, ex: `1`, `2`, `3`)|Código de build interno usado pelas lojas para gerenciar atualizações sequenciais.|

### 1. Estrutura no Arquivo `.csproj`

Ao editar o arquivo `.csproj` com um clique duplo no projeto, as configurações ficam agrupadas no bloco `<PropertyGroup>` principal:



```XML
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <TargetFrameworks>net8.0-android;net8.0-ios;net8.0-maccatalyst</TargetFrameworks>
        <TargetFrameworks Condition="$([MSBuild]::IsOSPlatform('windows'))">$(TargetFrameworks);net8.0-windows10.0.19041.0</TargetFrameworks>

        <OutputType>Exe</OutputType>
        <RootNamespace>NumeroDaSorte</RootNamespace>
        <UseMaui>true</UseMaui>
        <SingleProject>true</SingleProject>
        <ImplicitUsings>enable</ImplicitUsings>

        <!-- Configurações de Identidade e Exibição -->
        <ApplicationTitle>Número da Sorte</ApplicationTitle>
        <ApplicationId>br.com.spacebidu.numerodasorte</ApplicationId>
        <ApplicationIdGuid>A1B2C3D4-E5F6-7890-ABCD-EF1234567890</ApplicationIdGuid>

        <!-- Versionamento -->
        <ApplicationDisplayVersion>1.0.0</ApplicationDisplayVersion>
        <ApplicationVersion>1</ApplicationVersion>
    </PropertyGroup>

</Project>
```

### 2. Padrão de Identificador (Reverse Domain Notation)

O `ApplicationId` (conhecido como _Package Name_ no Android e _Bundle Identifier_ no iOS) impede colisões entre apps diferentes na loja:

- **Formato padrão:** `com.{empresa}.{nome_do_app}` ou `br.com.{empresa}.{nome_do_app}`
    
- **Exemplo real:**
    
    - Site da empresa: `spacebidu.com.br`
        
    - Nome do aplicativo: `NumeroDaSorte`
        
    - ID resultante: `br.com.spacebidu.numerodasorte` (sempre em letras minúsculas e sem caracteres especiais).
        

### 3. Versionamento: SemVer vs Build Code

As lojas de aplicativos exigem dois tipos distintos de versão a cada publicação:

```
Versão de Exibição (SemVer):   [ MAJOR ] . [ MINOR ] . [ PATCH ]
                                   ↓           ↓           ↓
                             Mudança Geral   Nova Feature   Correção de Bug
                             (Redesign total) (Ex: Lotomania) (Ex: erro cadastro)
                                  2.0.0          1.1.0           1.0.1

Versão Interna (Build Code):    [ INTEIRO INCREMENTAL: 1, 2, 3, 4... ]
```

|**Tipo de Alteração**|**Exemplo no App**|**ApplicationDisplayVersion**|**ApplicationVersion (Build)**|
|---|---|---|---|
|**Lançamento Inicial**|Primeira versão pública na loja|`1.0.0`|`1`|
|**Hotfix / Bug**|Correção de erro na validação|`1.0.1`|`2`|
|**Nova Funcionalidade**|Adição de jogos de Lotofácil e Lotomania|`1.1.0`|`3`|
|**Reestruturação Completa**|Redesign total da interface e arquitetura|`2.0.0`|`4`|

### 4. Propagação Nativa Automática

O .NET MAUI injeta os valores do `.csproj` diretamente nos arquivos específicos de cada plataforma durante o build:

- **Android (`Platforms/Android/AndroidManifest.xml`):**
    
    - Define `android:versionCode` a partir de `$(ApplicationVersion)`.
        
    - Define `android:versionName` a partir de `$(ApplicationDisplayVersion)`.
        
    - Define `package` a partir de `$(ApplicationId)`.
        
- **iOS (`Platforms/iOS/Info.plist`):**
    
    - Define `CFBundleVersion` (Build) a partir de `$(ApplicationVersion)`.
        
    - Define `CFBundleShortVersionString` a partir de `$(ApplicationDisplayVersion)`.
        
    - Define `CFBundleIdentifier` a partir de `$(ApplicationId)`.